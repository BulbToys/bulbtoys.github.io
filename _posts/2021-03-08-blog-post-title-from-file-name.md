## Blog Post Title From First Header

Due to a plugin called `jekyll-titles-from-headings` which is supported by GitHub Pages by default. The above header (in the markdown file) will be automatically used as the pages title.

If the file does not start with a header, then the post title will be derived from the filename.

This is a sample blog post. You can talk about all sorts of fun things here.

---

### This is a header

#### Diff test

```diff
= ctf_haarp
= ctf_helltrain_event
- ctf_minetest
+ workshop/ctf_minetest2.ugc3140160253
= ctf_system_rc1
= ctf_turbine
```

#### C++ test

```cpp
const char* BulbToys::Meow()
{
	return "mrrrp :3";
}
```

#### AHK test

```autohotkey
#MaxThreadsPerHotkey 3

!F8::
Toggle := !Toggle
Loop
{
	If (!Toggle)
		Break
	SendInput {W down}
	Sleep 300
	SendInput {W up}
	Sleep 5000
	SendInput {S down}
	Sleep 150
	SendInput {S up}
	Sleep 150
	SendInput {2 down}
	Sleep 150
	SendInput {2 up}
}
Return
```

