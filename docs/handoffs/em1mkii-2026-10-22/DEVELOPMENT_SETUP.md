# Development setup and rebuild

Install Git, Android Studio and its Android SDK, and a compatible Java 17 JDK on the replacement Windows PC. The existing workflow uses Ubuntu and Temurin Java 17; dependency and Android SDK requirements are defined by the checked-in Gradle configuration. Network access is needed for Gradle dependencies.

Clone `https://github.com/80spizzarat/db_link_EM-1_MkII.git`, then check out commit `0d4e947a5286228d5b75158367c82d8b2b316952` on a new working branch. Verify `git rev-parse HEAD`. Alternatively clone the preserved Git bundle and verify the same SHA and local known-good tag. Never overwrite the known-good ref with a later experiment.

The recorded GitHub workflow runs `./gradlew :app:testDebugUnitTest :app:assembleDebug -Dorg.gradle.java.home="$JAVA_HOME" -PDBLINK_BUILD_ROOT=$GITHUB_WORKSPACE/build-output` and uploads `build-output/outputs/apk/debug/*.apk`. Windows uses `gradlew.bat` and an appropriate writable output path. A future rebuild is not asserted to be byte-identical or camera-qualified. Preserve existing installed apps and photographs; only install a diagnostic after confirming its package identity and owner approval.

