# IceHook
very basic and minimalistic hooking "library" for windows (x64 support soon)

Example how to use:
```cpp
typedef void(__stdcall* twglSwapBuffers)(HDC hdc);
HookSettings wgl_swap_buffers_info;

void __stdcall hwglSwapBuffers(HDC hdc) {
	std::cout << "hooked\n";

	return reinterpret_cast<twglSwapBuffers>(wgl_swap_buffers_info.gateway)(hdc);
}

void hooks::InitWglSwapBuffers(){
	void* addr = (twglSwapBuffers)(GetProcAddress(GetModuleHandleA("opengl32.dll"), "wglSwapBuffers"));
	
	wgl_swap_buffers_info.src = addr;
	wgl_swap_buffers_info.dst = hwglSwapBuffers;
	wgl_swap_buffers_info.size = 5;

	Hook(wgl_swap_buffers_info);
}

void hooks::UnInitWglSwapBuffers() {
	UnHook(wgl_swap_buffers_info);
}
```
<h2>Author: Freshy</h2>
