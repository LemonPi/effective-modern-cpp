## alias declarations
- better than typedefs
	- works with templates
	- avoids ::type suffix and typename prefix
		- typedefs need typename prefix for templates because Widget<T>::type could refer to data member
			- some specialization of Widget could define type to be a data member
			- need assertion that it refers to a type
- C++14 offers alias type transformations
	- instead of typename std::remove_const<T>::type use std::remove_const_t<T>