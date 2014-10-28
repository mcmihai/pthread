Simple pthreads
===============

http://github.com/rmitton/pthread

This is a simple pthreads implementation for Windows, targeting Vista and upwards.

The goals of this library are:

- A simple, high-quality, standalone implementation of the POSIX pthreads API.
- Minimalistic - just a single .c file and the 1 or 2 header files required. Easy to drop
  into any project.
- No awkward licensing issues. This is released as completely free software to use as you wish. 
  You do not have to credit anybody or comply with any licensing restrictions. (see UNLICENSE)
- No undocumented APIs. This is implemented entirely using standard Win32 APIs.
- Don't invent our own threading primitives which won't work. Writing thread primitives is very hard,
  and even experts often get it wrong and introduce race conditions. We use the existing OS whenever possible,
  to make our implementation provably correct. When we have to make our own, we write them in terms of
  other existing tested OS primitives.

To use this library, simply grab the .c and .h files and throw them into your own project.
No complicated build system is required.

If you do wish for a DLL, project files and Makefiles for Visual Studio and mingw are provided.

## NOTES

- Thread cancellation isn't really supported much. It's kind of a damn-stupid thing to be doing anyway,
  (especially the async version, which is just plain dangerous). Deferred cancellation *is* fully
  supported, except the only cancellation points provided are `pthread_join`, manual calls to `thread_testcancel`, and 
  any **alertable** Win32 function (e.g. `SleepEx`, `WaitForSingleObjectEx`).
- Most of the timeout-based functions are not supported. It doesn't entirely make sense, as POSIX mandates
  the timer to be clocked against the POSIX system clock, which Windows doesn't even have.
