# Maven
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/auth/login").permitAll()
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .requestMatchers("/vendas/**").hasAnyRole("VENDEDOR","ADMIN")
                .anyRequest().authenticated()
            )
            .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));

        http.addFilterBefore(jwtFilter(), UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }
}
mvn clean package
target/seu-projeto-0.0.1-SNAPSHOT.jar
java -jar target/seu-projeto.jar
nohup java -jar seu-projeto.jar &
nohup java -jar seu-projeto.jar > app.log 2>&1 &FROM eclipse-temurin:21
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
docker build -t meuapp .docker run -d -p 8080:8080 meuapp
heroku create
git push heroku main
