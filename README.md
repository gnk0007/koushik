package com.pawsos.pawsosbackend.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers(
                    "/api/users/**",
                    "/api/pets/**",
                    "/api/stray/**",
                    "/api/helpcenters/**",
                    "/api/sos/**",
                    "/api/volunteers/**",
                    "/api/appointments/**",
                    "/api/adoption/**",
                    "/api/fundraisers/**",
                    "/api/donations/**",
                    "/api/medications/**",
                    "/api/vets/**",
                    "/api/prescriptions/**",
                    "/api/lostpets/**",
                    "/api/boarding/**"
                ).permitAll()
                .anyRequest().authenticated()
            )
            .httpBasic(Customizer.withDefaults());

        return http.build();
    }
}