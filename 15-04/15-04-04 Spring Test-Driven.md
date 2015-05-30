
### Mock Autowired Objects During Test

[Use MockitoJUnitRunner](https://ahlearns.wordpress.com/2012/03/02/spring-3-autowired-unit-tests-with-mockito/)

```java
// Impl
@Service
public class SupervisorService {

    @Autowired private SupervisorDAO supervisorDao;

    @Transactional(readOnly=true)
    public List getSupervisors() {
        return supervisorDao.getSupervisors();
    }

    /**
     * Determine if the supervisor is responsible for any users for the
     * specified department
     * @param dbId The dbId of the supervisor
     * @param department The department to look for
     * @return true if there are users assigned to the superivsor for the department
     */
    public boolean isSupervisorResponsibleForUser(int dbId, String department) {
        if (dbId == 0) {
            throw new IllegalArgumentException("A dbId is required");
        }
        if (department == null) {
            throw new IllegalArgumentException("department is required");
        }
        boolean hasUsers = false;
        int numAssignedUsers = supervisorDao.getUserCountForSupervisor(dbId, department);
        if (numAssignedUsers > 0) {
            hasUsers = true;
        }
        return hasUsers;
    }
}

// Test

@RunWith(MockitoJUnitRunner.class)
public class SupervisorServiceUnitTest {

    @Mock private SupervisorDAO mockSupervisorDao;
    @InjectMocks private SupervisorService supervisorService;

    @Before
    public void init() {
        when(mockSupervisorDao.getUserCountForSupervisor(1, "Department1"))
            .thenReturn(2);
        when(mockSupervisorDao.getUserCountForSupervisor(1, "Department2"))
            .thenReturn(0);
    }

    @Test
    public void testIsSupervisorResponsibleForUserTrue() {
        boolean isSupervisor = supervisorService.isSupervisorResponsibleForUser(1, "Department1");
        assertTrue(isSupervisor);
    }

    @Test
    public void testIsSupervisorResponsibleForUserFalse() {
        boolean isSupervisor = supervisorService.isSupervisorResponsibleForUser(1, "Department2");
        assertFalse(isSupervisor);
    }

    @Test(expected=IllegalArgumentException.class)
    public void testIsSupervisorResponsibleRequiredDbId() {
        supervisorService.isSupervisorResponsibleForUser(0, "Department3");
    }

    @Test(expected=IllegalArgumentException.class)
    public void testIsSupervisorResponsibleRequiredDivision() {
        supervisorService.isSupervisorResponsibleForUser(1, null);
    }
}

```



### @Before vs @BeforeClass

[Link](http://examples.javacodegeeks.com/core-java/junit/junit-before-and-beforeclass-example/)


- `@Before`: annotation indicates that this method must be executed before each test in the class, so as to execute some preconditions necessary for the test.

- `@BeforeClass`: annotation indicates that the static method to which is attached must be executed once and before all tests in the class. That happens when the test methods share computationally expensive setup (e.g. connect to database).
