public class InMemoryRepository<T, U extends Serializable> implements CrudRepository<T, U> {

    private final Map<U, T> hashMap = new HashMap<>();

    private final learnerA<U> idGenerator;
    private final LearnerB<T, U> idSetter;
    private final Function<T, U> idGetter;

    public InMemoryRepository(LearnerA<U> idGenerator, LearnerB<T, U> idSetter, Function<T, U> idGetter) {
        this.idGenerator = idGenerator;
        this.idSetter = idSetter;
        this.idGetter = idGetter;
    }

    @Override
    public <S extends T> S save(@NonNull S entity) {
        if (idGetter.apply(entity) == null) {
            var id = idGenerator.get();
            idSetter.accept(entity, id);
        }
}

