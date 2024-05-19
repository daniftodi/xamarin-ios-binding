
xcodebuild -project "Extole-iOS/Extole-iOS.xcodeproj" archive \
  -scheme "Extole-iOS" \
  -configuration Release \
  -archivePath "build/Extole-iOS-simulator.xcarchive" \
  -destination "generic/platform=iOS Simulator" \
  -derivedDataPath "build" \
  -IDECustomBuildProductsPath="" -IDECustomBuildIntermediatesPath="" \
  ENABLE_BITCODE=NO \
  SKIP_INSTALL=NO \
  BUILD_LIBRARY_FOR_DISTRIBUTION=YES

xcodebuild -project "Extole-iOS/Extole-iOS.xcodeproj" archive \
   -scheme "Extole-iOS" \
   -configuration Release \
   -archivePath "build/Extole-iOS-ios.xcarchive" \
   -destination "generic/platform=iOS" \
   -derivedDataPath "build" \
   -IDECustomBuildProductsPath="" -IDECustomBuildIntermediatesPath="" \
   ENABLE_BITCODE=NO \
   SKIP_INSTALL=NO \
   BUILD_LIBRARY_FOR_DISTRIBUTION=YES

xcodebuild -create-xcframework \
                -framework "build/Extole-iOS-ios.xcarchive/Products/Library/Frameworks/Extole_iOS.framework" \
                -framework "build/Extole-iOS-simulator.xcarchive/Products/Library/Frameworks/Extole_iOS.framework" 

sharpie bind --sdk=iphoneos16.2 --output="XamarinApiDef" --namespace="ExtoleiOSLibBinding" --scope="Extole_iOS.xcframework/ios-arm64/Extole_iOS.framework/Headers/" "build/Extole_iOS.xcframework/ios-arm64/Extole_iOS.framework/Headers/Extole_iOS.h";
