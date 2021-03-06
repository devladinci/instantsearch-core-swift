Maintenance
===========

*Note: this documentation is for maintainers only. If you don't plan to hack the source code, you don't need to read this.*



## Objective-C bridgeability

Because we must guarantee that every feature is usable from Objective-C, and because not every Swift construct can be mapped to an Objective-C type, we must impose ourselves some restrictions:

- **Value types** cannot be used; or they must be provided as syntactic sugar (i.e. there must be another way to access the feature from Objective-C).

- **Default argument values** cannot be used; or an alternative form of the method must be provided for use from Objective-C.



## Deployment

### Deployment process

- Update the **version number** in:

    - `InstantSearch-Core-Swift.podspec`

    - `InstantSearch-Core-Offline-Swift.podspec`

    - `Sources/Info.plist` (or via Xcode, in the project settings)

- Update the **change log** (`ChangeLog.md`)

- **Dry-run the pod spec**: `pod lib lint` to check that everything's fine.

- Check-out the `gh-pages` branch into the `doc/build` directory:

    ```
    git clone git@github.com:algolia/instantsearch-core-swift -b gh-pages --single-branch doc/build
    ```

- Generate the **documentation**: `tools/make-doc.sh`

    *Note: requires [Jazzy](https://github.com/realm/jazzy).*

- **Push to GitHub**:

    ```
    git commit -m "Version X.Y.Z"
    git tag X.Y.Z
    git push --tags origin master
    ```

- Make sure you have a **CocoaPods session** open: `pod trunk me`. If you have no active session, use
  `pod trunk register EMAIL` to create one. (If you have never registered to CocoaPods, you need to contact one of
  the pod's owners; `pod trunk info` is your friend.)

- **Publish the pod:**

    - `pod trunk push InstantSearch-Core-Swift.podspec`

    - `pod trunk push InstantSearch-Core-Offline-Swift.podspec`

- Edit the **release notes**: in GitHub, edit the tag and copy-paste the Change Log section for this release.

- **Publish the documentation** to GitHub pages: `cd doc/build && git push`

- Update the **external documentation** if necessary:

    - [Guides](https://www.algolia.com/doc/guides)
    - [FAQ](https://www.algolia.com/doc/faq)


### Documentation

Documentation is generated by [Jazzy](https://github.com/realm/jazzy). Of course you will need to install it first: `sudo gem install jazzy` should do the trick.

Generating the documentation is as simple as running:

```
jazzy --clean
```
