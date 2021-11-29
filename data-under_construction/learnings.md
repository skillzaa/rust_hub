# Learning 2021-Oct-28 

There is a difference between creating a *trait* and creating an *impl* block for a struct etc. In trait you do not have to mention each method as *pub* since it is understood. However in case of an imple block you have to mention what is public and what is not, since the impl block will contain the  publis as well as privte function of a struct etc.
While creating an **impl** block keep in mind that all the functions that do not get a **&self** will be act as *associated methods*.
Rust does not support C++ type function overloading.It means that we can not have 2 functions with same names but different argumants. *A solution for this is using tuples with different values*.
The ToString is a useful trait that has the *to*
