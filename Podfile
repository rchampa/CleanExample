# Uncomment the next line to define a global platform for your project
# platform :ios, '9.0'

platform :ios, '13.6'

workspace 'CleanExample'
use_frameworks!

def firebase_pods
  pod 'Firebase/Core', '7.11.0'
  pod 'Firebase/Auth', '7.11.0'
  pod 'Firebase/Firestore', '7.11.0'
  pod 'Firebase/Storage', '7.11.0'
  pod 'FirebaseFirestoreSwift', '7.11.0-beta'
end


target 'CleanExample' do
  project 'CleanExample'
  firebase_pods
  pod 'FirebaseUI/Storage'
end

target 'PresentationCleanExample' do
  project 'PresentationCleanExample/PresentationCleanExample.xcodeproj'
#  firebase_pods
  pod 'FirebaseUI/Storage'
end

target 'DomainCleanExample' do
  project 'DomainCleanExample/DomainCleanExample.xcodeproj'
end

target 'DataCleanExample' do
  project 'DataCleanExample/DataCleanExample.xcodeproj'
  firebase_pods
end

post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
        end
    end
end
