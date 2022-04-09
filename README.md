# gem-rbs

Collection of RBS definitions for gems we use, meant to be incorporated with Steep through `rbs collection`. Similar to [ruby/gem_rbs_collection](https://github.com/ruby/gem_rbs_collection), this contains generated type definitions for third party gems. This is meant to be used in conjuction with `ruby/gem_rbs_collection`, so it only adds additional definitions not already defined there.

## Adding these types for use in another library

Add the following to your `rbs_collection` configuration file:

```yaml
sources:
  # ... your other sources
  - name: Shelf-Life/gem-rbs
    remote: https://github.com/Shelf-Life/gem-rbs.git
    revision: main
    repo_dir: gems

```

Run `rbs collection update` and you should be good to go. If you haven't configured `rbs collection`, see the instructions [here](https://github.com/ruby/rbs/blob/master/docs/collection.md).

## Adding/updating new definitions to this library

Fork/create a new branch. If adding a new gem (or definitions for a new version), create the appropriate folders in `gems`:

```sh
mkdir ./gems/gem-name && mkdir ./gems/gem-name/1.2
```

Version folders should only use major/minor revisions.

Once you have created the folders, run `rbs prototype` for the library you wish to generate:

```sh
rbs prototype rb path/to/gem-source-location/gem-name-1.2/lib/**/*.rb > path/to/this/repo/gems/gem-name/1.2/gem-name-generated.rbs
```

Push your changes to GitHub. Using another project relying on this for your gems, update the `rbs_collection` configuration to point to your fork/branch of this repo instead of main, and run `rbs collection update`. Iterate on your definitions until `steep check` passes (`rbs prototype` does not always generate completely correct definitions).

Once you are finished, create a pull request to merge your changes back to main.
