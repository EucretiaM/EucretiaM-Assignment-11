class StorageManager {
    constructor() {
        this.backends = {};
    }

    registerBackend(name, backend) {
        this.backends[name] = backend;
    }

    async store(backendName, key, data) {
        if (!this.backends[backendName]) {
            throw new Error(`Storage backend "${backendName}" not registered.`);
        }
        return this.backends[backendName].store(key, data);
    }

    async retrieve(backendName, key) {
       if (!this.backends[backendName]) {
            throw new Error(`Storage backend "${backendName}" not registered.`);
        }
        return this.backends[backendName].retrieve(key);
    }

    async delete(backendName, key) {
        if (!this.backends[backendName]) {
            throw new Error(`Storage backend "${backendName}" not registered.`);
        }
        return this.backends[backendName].delete(key)
    }
}

const storageManager = new StorageManager();

