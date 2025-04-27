package com.proitr.camunda.demo.repository;


import lombok.NonNull;
import org.springframework.data.repository.CrudRepository;
import java.io.Serializable;
import java.util.*;
import java.util.function.BiConsumer;
import java.util.function.Function;
import java.util.function.Supplier;
import java.util.stream.Collectors;

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

        var id = idGetter.apply(entity);
        hashMap.put(id, entity);
        return entity;
    }

    @Override
    public <S extends T> Iterable<S> saveAll(@NonNull Iterable<@NonNull S> list) {
        list.forEach(this::save);
        return list;
    }

    @Override
    public Optional<T> findById(U id) {
        return Optional.ofNullable(hashMap.get(id));
    }

    @Override
    public boolean existsById(U id) {
        return hashMap.containsKey(id);
    }

    @Override
    public Iterable<T> findAll() {
        return hashMap.values();
    }

    @Override
    public Iterable<T> findAllById(@NonNull Iterable<@NonNull U> list) {
        var idList = new ArrayList<U>();
        list.forEach(idList::add);
        return hashMap.values().stream()
                .filter(item -> idList.contains(idGetter.apply(item)))
                .collect(Collectors.toList());
    }

    @Override
    public long count() {
        return hashMap.size();
    }

    @Override
    public void deleteById(U id) {
        hashMap.remove(id);
    }
