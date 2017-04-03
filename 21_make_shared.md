## make_shared
- prefer std::make_shared to passing new ptr to std::shared_ptr constructor
	- prevent code duplication
		- don't have to specify type twice
	- more efficient
		- constructor with new method allocates to heap twice
			- once for object
			- once for control block
			- additional overhead
		- make_shared makes one allocation
			- control block allocated after object
			- links control block's lifetime to object's lifetime
				- potentially inefficient if weak_ptr are around after object has died
					- control block can't be destroyed if weak_ptrs point to it
					- unlikely scenario though 
	- exception safe
		- constructor with new method calls 2 constructors
			- first for new object
			- then for shared_ptr taking the moved object
			- unsafe when used together with another expression that could throw
				- f(std::shared_ptr<Widget>(new Widget), computePriority())
					- 3 operations in total
						- order not deterministic
					- computePriority() could throw
						- if computePriority executed between new and shared_ptr construction then leak could happen
- in C++11, roll own make_unique by perfect forwarding
	- template<typename T, typename... Ts> 
	std::unique_ptr<T> make_unique(Ts&&... params) { 
		return std::unique_ptr<T>(new T(std::forward<Ts>(params)...)); 
	}