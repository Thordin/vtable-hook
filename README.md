vtable-hook
===========

C++ Vtable Hooking Library. Only requires a header.

Supports Windows and Linux.

### Example ###
```C++
#include "vtablehook.h"
#include <stdio.h>

class Object {
        public:
        int member;

        Object(int init) {
                member = init;
        }

        virtual void Foo() {
                printf("Bar\n");
        }
};

#ifdef WIN32
void __fastcall FooHook(Object* that) {
#elif __linux__
void FooHook(Object* that) {
#endif
        printf("Hooked %i\n", that->member);
}

int main() {
        Object* o = new Object(123);
        o->Foo();

        vtablehook_hook(o, (void*)FooHook, 0);
        o->Foo();

        return 0;
}

```