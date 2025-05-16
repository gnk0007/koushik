package com.pawsos.pawsosbackend.entity;

import jakarta.persistence.*;
import lombok.*;
import java.time.LocalDate;

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Medication {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String dosage;
    private String frequency;
    private LocalDate startDate;
    private LocalDate endDate;
    private LocalDate expiryDate;
    private String notes;

    @ManyToOne
    @JoinColumn(name = "pet_id")
    private Pet pet;
}




package com.pawsos.pawsosbackend.dto;

import lombok.*;
import java.time.LocalDate;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class MedicationDTO {
    private Long petId;
    private String name;
    private String dosage;
    private String frequency;
    private LocalDate startDate;
    private LocalDate endDate;
    private LocalDate expiryDate;
    private String notes;
}



package com.pawsos.pawsosbackend.repository;

import com.pawsos.pawsosbackend.entity.Medication;
import org.springframework.data.jpa.repository.JpaRepository;

public interface MedicationRepository extends JpaRepository<Medication, Long> {
}



package com.pawsos.pawsosbackend.service;

import com.pawsos.pawsosbackend.dto.MedicationDTO;
import com.pawsos.pawsosbackend.entity.Medication;
import com.pawsos.pawsosbackend.entity.Pet;
import com.pawsos.pawsosbackend.repository.MedicationRepository;
import com.pawsos.pawsosbackend.repository.PetRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class MedicationService {

    @Autowired
    private MedicationRepository medicationRepository;

    @Autowired
    private PetRepository petRepository;

    public String addMedication(MedicationDTO dto) {
        Pet pet = petRepository.findById(dto.getPetId())
                .orElseThrow(() -> new RuntimeException("Pet not found"));

        Medication medication = new Medication();
        medication.setPet(pet);
        medication.setName(dto.getName());
        medication.setDosage(dto.getDosage());
        medication.setFrequency(dto.getFrequency());
        medication.setStartDate(dto.getStartDate());
        medication.setEndDate(dto.getEndDate());
        medication.setExpiryDate(dto.getExpiryDate());
        medication.setNotes(dto.getNotes());

        medicationRepository.save(medication);
        return "Medication added successfully!";
    }

    public List<Medication> getAllMedications() {
        return medicationRepository.findAll();
    }
}



package com.pawsos.pawsosbackend.controller;

import com.pawsos.pawsosbackend.dto.MedicationDTO;
import com.pawsos.pawsosbackend.entity.Medication;
import com.pawsos.pawsosbackend.service.MedicationService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/medications")
@CrossOrigin(origins = "*")
public class MedicationController {

    @Autowired
    private MedicationService medicationService;

    @PostMapping("/add")
    public String addMedication(@RequestBody MedicationDTO dto) {
        return medicationService.addMedication(dto);
    }

    @GetMapping("/all")
    public List<Medication> getAll() {
        return medicationService.getAllMedications();
    }
}




{
  "petId": 1,
  "name": "Metacam",
  "dosage": "5ml",
  "frequency": "Once daily",
  "startDate": "2024-05-10",
  "endDate": "2024-05-20",
  "expiryDate": "2025-01-01",
  "notes": "Anti-inflammatory medication"
}



