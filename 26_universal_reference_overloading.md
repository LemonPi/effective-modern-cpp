## universal_reference_overloading
- avoid overloading functions taking universal references
	- univeral reference overload will be called more frequently than expected
	- perfect forwarding constructors are better matches than copy constructors for non-const lvalues
		- hijacks derived class calls to base class copy and move constructors
- alternatives to overloading
	- use different name
	- pass by const T&
		- not as efficient since we might have to construct temporaries
	- pass by copy
	- tag dispatch
		- template<typename T> void logAndAdd(T&& name) {
			logAndAddImpl(std::forward<T>(name), std::is_integral<typename std::remove_reference<T>>::type>());
		}
		- then use std::false_type and std::true_type to overload
	- constrain template generation
		- constructor calls may be handled by compiler-generated functions that bypass tag dispatch
		- std::enable_if forces template generation only if true
			- uses SFINAE
		- template <typename T, 
					typename = typename std::enable_if<condition>::type>
			- condition is bool
				- many compile time checks provided by std
					- std::is_floating_point<T>::value
					- std::is_same<T, U>::value
					- std::is_integral<T>::value
					- std::is_trivially_constructible<T, Args&&...>::value
					- std::is_base_of<Parent, T>::value
					- can combine conditions
						- ! negation
						- && and
						- other boolean operations