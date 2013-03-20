Usage:
```lua
local PATH = require "path"

-- suppose we run on windows
assert(PATH.IS_WINDOWS)

-- we can use system dependet function
print(PATH.user_home())  -- C:\Documents and Settings\Admin
print(PATH.currentdir()) -- C:\lua\5.1

-- but we can use specific system path notation
local ftp_path = PATH.new('/')
print(ftp_path:join("/root", "some", "dir")) -- /root/some/dir

-- All functions specific to system will fail
assert(not pcall( ftp_path.currentdir, ftp_path ) )
```

```lua
-- clean currentdir

local path = require "path"
path.each("./*", function(P, mode)
  if mode == 'directrory' then 
    path.rmdir(P)
  else
    path.remove(P)
  end
end,{
  param = "fm";   -- request full path and mode
  delay = true;   -- use snapshot of directory
  recurse = true; -- include subdirs
  reverse = true; -- subdirs at first 
})
```