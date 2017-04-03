## weak_ptr
- for checking expiration of std::shared_ptr without owning a reference
- useful for caches which need to know if the distributed shared_ptrs need to be reloaded
- useful for observer pattern subjects that need to know if observers are still alive
- cannot dereference or check for null directly
	- use lock() method to return a std::shared_ptr
		- will be null if there are no more references
	- pass weak_ptr to std::shared_ptr constructor
		- will throw an exception if there are no more references