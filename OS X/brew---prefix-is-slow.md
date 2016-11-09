# `brew --prefix` is slow

So slow it takes a whole 0.04s and calling it with an argument is even slower, taking a whopping 0.3s on my machine.
I guess this isn't that slow, but if you're calling it multiple times in your `.zshrc` or `.bashrc` it all adds up.
To claw some of this speed back, run it once and assign it to a variable and then use the variable from then on.

If you've got scripts that pass the brew program as an argument to `brew --prefix`, e.g. `brew --prefix chruby` then
either cache them on a one off basis, or just replace it with `${BREW_PREFIX}/opt/chruby/` and it'll work the same way.
