1)
	a) number ✅
	b) string ✅
	c) 'pineapples' ✅
	d) [boolean, boolean, boolean] ❌ boolean[]
	e) {type: string} ✅
	f) [number, boolean] ❌ (number | boolean)[] 
	g) number[] ✅
	h) number ❌any

2
	a) The type is 3 and we are assigning 4 - i is type literal 3 and we are trying to assign type literal 4
	b) We are trying to push a string onto an array which has been assigned number types
	c) never is the bottom type and nothing is assignable to never
	d) Cannot use variables of type unknown, has to be refined to a more specific type by means of typeof, instanceof or another type of query or type guard