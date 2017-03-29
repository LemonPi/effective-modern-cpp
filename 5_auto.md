## auto
- prefer over explicit typing for efficiency and correctness
- do not use with invisible proxies (e.g. std::vector<bool>::reference from operator[])
	- static_cast<desired_type>(proxy) for this
- decltype(auto) means auto but using decltype rules instead of the default template deduction rules