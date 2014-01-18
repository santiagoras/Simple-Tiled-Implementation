Simple Tiled Implementation
==
---
Simple Tiled Implementation is a [**Tiled Map Editor**][Tiled] library designed for the *awesome* [**LÖVE**][LOVE] framework. Please read the library [**documentation**][dox] to learn how it all works!

Quick Example
--
---
```lua     
local sti = require "sti"

function love.load()
	-- Load a map exported to Lua from Tiled
	map = sti.new("assets/maps/map01")
	
	-- Create a Collision Map to use with your own collision code
	map:createCollisionMap("Collision Layer")
	
	-- Create a Custom Layer
	map:newCustomLayer("Sprite Layer", 3)
	
	-- Add data to Custom Layer
	local spriteLayer = map.layers["Sprite Layer"]
	spriteLayer.sprites = {
		player = {
			image = love.graphics.newImage("assets/sprites/player.png"),
			x = 64,
			y = 64,
			r = 0,
		}
	}
	
	-- Update callback for Custom Layer
	function spriteLayer:update(dt)
		for _, sprite in pairs(self.sprites) do
			sprite.r = sprite.r + 90 * dt
		end
	end
	
	-- Draw callback for Custom Layer
	function spriteLayer:draw()
		for _, sprite in pairs(self.sprites) do
			local x = math.floor(sprite.x)
			local y = math.floor(sprite.y)
			local r = math.rad(sprite.r)
			love.graphics.draw(sprite.image, x, y, r)
		end
	end
end

function love.update(dt)
	map:update(dt)
end

function love.draw()
	map:draw()
	
	-- Draw Collision Map (useful for debugging)
	map:drawCollisionMap()
end

```

License
--
---
This code is licensed under the [**MIT Open Source License**][MIT]. Check out the LICENSE file for more information.

[Tiled]:	http://www.mapeditor.org/
[LOVE]:		https://www.love2d.org/
[dox]:		http://karai17.github.io/Simple-Tiled-Implementation/
[MIT]:		http://www.opensource.org/licenses/mit-license.html