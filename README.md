# Framework-dSYM-test

Example project to demonstrate changes for https://github.com/fastlane/gym/pull/114

# Usage
*Note* You may have to adjust code-signing information/bundle indentifier to get a project that you can personally archive.

## With Frameworks
1. Run `bundle install` (this will install the patched version of Gym)
2. Run `be gym --scheme Framework-dSYMs`

After the archive has been created you should see a log message that looks a bit like...

```
Compressing 4 dSYM(s)
```

## Without Frameworks
1. Remove the `use_frameworks!` line from the `Podfile`
2. Run `pod install`
3. Run `be gym --scheme Frameworks-dSYMs`

After the archive has been created you should see a log message that looks a bit like...

```
Compressing 1 dSYM(s)
```

# Why does this matter?

If you're using a development pod in order to produce a framework for multiple targets within the same project, the unpatched version of Gym would not pick up all required dSYM files that are required to produce symbolicated reports of the shared framework.

Ideally, if there is 1 dSYM, there _could_ be more than one, so we should be greedy when trying to find them.
