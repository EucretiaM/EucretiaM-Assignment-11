public class InMemoryRepository<T, U extends Serializable> implements CrudRepository<T, U> {

    private final Map<U, T> hashMap = new HashMap<>();

    private final Supplier<U> idGenerator;
    private final BiConsumer<T, U> idSetter;
    private final Function<T, U> idGetter;

    public InMemoryRepository(Supplier<U> idGenerator, BiConsumer<T, U> idSetter, Function<T, U> idGetter) {
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

