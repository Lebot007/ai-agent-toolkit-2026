# Java Spring Boot - Desenvolvimento Backend

## O que e
Framework Java para criar aplicacoes backend rapidamente.

## Setup Basico

### Projeto com Spring Initializr
Acessar start.spring.io e selecionar:
- Project: Maven/Gradle
- Language: Java
- Spring Boot: 3.x
- Dependencies: Spring Web, Spring Data JPA, PostgreSQL

### Estrutura do Projeto
src/
  main/
    java/
      com/example/demo/
        DemoApplication.java
        controller/
        service/
        repository/
        entity/
    resources/
      application.properties

## Controllers

### REST Controller Basico
@RestController
@RequestMapping('/api/users')
public class UserController {
    
    @GetMapping
    public List<User> getAllUsers() {
        return userService.findAll();
    }
    
    @GetMapping('/{id}')
    public ResponseEntity<User> getUserById(@PathVariable Long id) {
        return userService.findById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }
    
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.save(user);
    }
    
    @PutMapping('/{id}')
    public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody User user) {
        return userService.update(id, user)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }
    
    @DeleteMapping('/{id}')
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        userService.delete(id);
        return ResponseEntity.noContent().build();
    }
}

### Request Parameters
@GetMapping('/search')
public List<User> searchUsers(
    @RequestParam String name,
    @RequestParam(defaultValue = '0') int page,
    @RequestParam(defaultValue = '10') int size) {
    return userService.search(name, page, size);
}

## Services

### Service Layer
@Service
@Transactional
public class UserService {
    
    @Autowired
    private UserRepository userRepository;
    
    public List<User> findAll() {
        return userRepository.findAll();
    }
    
    public Optional<User> findById(Long id) {
        return userRepository.findById(id);
    }
    
    public User save(User user) {
        return userRepository.save(user);
    }
    
    public Optional<User> update(Long id, User user) {
        return userRepository.findById(id)
            .map(existing -> {
                existing.setName(user.getName());
                existing.setEmail(user.getEmail());
                return userRepository.save(existing);
            });
    }
    
    public void delete(Long id) {
        userRepository.deleteById(id);
    }
}

## Repositories

### JPA Repository
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    List<User> findByName(String name);
    
    List<User> findByEmailContaining(String email);
    
    @Query('SELECT u FROM User u WHERE u.age > :age')
    List<User> findUsersOlderThan(@Param('age') int age);
    
    @Query(value = 'SELECT * FROM users WHERE created_at > :date', nativeQuery = true)
    List<User> findUsersCreatedAfter(@Param('date') LocalDate date);
}

## Entities

### JPA Entity
@Entity
@Table(name = 'users')
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    @Column(unique = true, nullable = false)
    private String email;
    
    @Column(name = 'created_at')
    private LocalDateTime createdAt;
    
    // Getters and setters
}

### Relationships
@Entity
public class Order {
    @Id
    @GeneratedValue
    private Long id;
    
    @ManyToOne
    @JoinColumn(name = 'user_id')
    private User user;
    
    @OneToMany(mappedBy = 'order', cascade = CascadeType.ALL)
    private List<OrderItem> items;
}

## Configuration

### application.properties
spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.username=user
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

### Profiles
application-dev.properties
application-prod.properties

spring.profiles.active=dev

## Security

### Spring Security
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers('/api/public/**').permitAll()
                .anyRequest().authenticated()
            )
            .httpBasic();
        return http.build();
    }
}

## Best Practices

### Estrutura
- Separar responsabilidades (controller, service, repository)
- Usar DTOs para requests/responses
- Validar inputs
- Tratar exceptions globalmente

### Performance
- Usar pagination para listas grandes
- Lazy loading de relationships
- Cache quando apropriado
- Connection pooling

### Testing
- Unit tests para services
- Integration tests para controllers
- Mock repositories quando necessario

## Quando Usar
- Aplicacoes backend robustas
- APIs REST
- Microservices
- Aplicacoes enterprise