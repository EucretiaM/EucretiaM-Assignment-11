/ Interface
interface IRepository {
    List<Object> getAll();
    Object getById(int id);
    void save(Object object);
    void update(Object object);
    void delete(int id);
}

// Concrete Implementations
class FileRepository implements IRepository {
    @Override
    public List<Object> getAll() {
        // Logic to read data from files
        return null;
    }
    // ... other methods
}

class DatabaseRepository implements IRepository {
    @Override
    public List<Object> getAll() {
        // Logic to query data from a database
        return null;
    }
    // ... other methods
}

// Factory
class RepositoryFactory {
    public static IRepository getRepository(String storageType) {
        if ("file".equalsIgnoreCase(storageType)) {
            return new FileRepository();
        } else if ("database".equalsIgnoreCase(storageType)) {
            return new DatabaseRepository();
        }
        throw new IllegalArgumentException("Unsupported storage type: " + storageType);
    }
}

// Client Usage
public class Main {
    public static void main(String[] args) {
        IRepository repository = RepositoryFactory.getRepository("database");
        List<Object> allObjects = repository.getAll();
        System.out.println(allObjects);
    }
}
