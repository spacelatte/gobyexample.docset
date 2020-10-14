
# GoByExample Dash DocSet

This is copy of [gobyexample](https://gobyexample.com) adapted for Dash.

Dash is a macOS documentation viewer with offline capabilities. As you can see,
it's pretty easy to extend and add custom HTML based documentation into the app.

## How to use

1. Clone this repository with submodules:
  `git clone --recursive https://github.com/pvtmert/gobyexample.docset`
  If you missed `--recursive` by mistake, you can do
  `git submodule update --init --recursive`

2. Create/initialize indexes using `make -C Contents index`

3. Add this to the Dash;
  - Open Dash,
  - Open Preferences (`CMD+,`),
  - In DocSets tab,
  - Click little `+` button on lower-left corner,
  - Select `Add local Docset`,
  - Point to this repository.

## How is this repo works.

Firstly, when cloned, thanks to magic of [`Info.plist`](Contents/Info.plist) and
`.docset` extension, Dash will be handling it if installed properly.

I did not wanted to clutter up repository by including SQLite3 indexes. Also
they might change in the future in upstream repository.

The upstream repository added as submodule, in order to update it,
you can execute `make -C Contents update`.

- Use `make -C Contents clean` to remove index.
- Use `make -C Contents index` to create index.

> Note: index re-creation needed after updating submodule.

## How index getting created

Upstream repository already includes prebuild HTML files inside the `public`
directory in it's root.

There is a file called
[`examples.txt`](Contents/Resources/gobyexample.git/examples.txt),
which contains page titles each line.

Even though this is not a stable and reliable way to extract, their convention
is just removing punctuation, adding dashes (`-`) instead of spaces to the
lowercased title.

> So, `Exec'ing Processes` becomes `execing-processes`.

The `index` rule of [`makefile`](makefile) creates necessary tables and
constraints. Then loops over the
[`examples.txt`](Contents/Resources/gobyexample.git/examples.txt) to generate
proper SQL with basic shell utilities.

## Reporting Bugs...

As in any software, bugs are highly probable and scared of light. If you find
them, please open a issue with a list of steps to reproduce.

If you also fix them, pull-requests are very-much welcome!

## License

Do whatever you want. I neither own Dash or gobyexample. Keep in mind that
Dash is neither free-software nor open-source. It has trial period and nags you
with your time after that period ends. However you can use it as long as you
want.

> You should consult respective repositories and their owners regarding
> permissions.
