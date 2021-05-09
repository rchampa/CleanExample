# Uncomment the next line to define a global platform for your project
# platform :ios, '9.0'
# Inspired by https://medium.com/@GalvinLi/tinysolution-fix-cocoapods-duplicate-implement-warning-5a2e1a505ea8

platform :ios, '13.6'

workspace 'CleanExample'
use_frameworks!

def data_pods
  pod 'Firebase/Core', '7.11.0'
  pod 'Firebase/Auth', '7.11.0'
  pod 'Firebase/Firestore', '7.11.0'
  pod 'Firebase/Storage', '7.11.0'
  pod 'FirebaseFirestoreSwift', '7.11.0-beta'
end

def presentation_pods
  pod 'FirebaseUI/Storage', '10.0.2'
  pod 'Firebase/Storage', '7.11.0'
  pod 'lottie-ios'
end

target 'CleanExample' do
  project 'CleanExample'
  presentation_pods
  data_pods
  
end

target 'PresentationCleanExample' do
  project 'PresentationCleanExample/PresentationCleanExample.xcodeproj'
  presentation_pods
end

target 'DomainCleanExample' do
  project 'DomainCleanExample/DomainCleanExample.xcodeproj'
end

target 'DataCleanExample' do
  project 'DataCleanExample/DataCleanExample.xcodeproj'
  data_pods
end

post_install do |installer|
  removeOTHERLDFLAGS(['PresentationCleanExample', 'DataCleanExample'], installer)
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
      config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
      config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
    end
  end
end



def removeOTHERLDFLAGS(target_names, installer)
  pods_targets_names = target_names.map{ |str| 'Pods-' + str }
  handle_app_targets(pods_targets_names, installer)
end

def find_line_with_start(str, start)
  str.each_line do |line|
    if line.start_with?(start)
      return line
    end
  end
  return nil
end

def remove_words(str, words)
  new_str = str
  words.each do |word|
    new_str = new_str.sub(word, '')
  end
  return new_str
end

def handle_app_targets(names, installer)
  puts "handle_app_targets"
  puts "names: #{names}"
  installer.pods_project.targets.each do |target|
    if names.index(target.name) == nil
      next
    end
    puts "Updating #{target.name} OTHER_LDFLAGS"
    target.build_configurations.each do |config|
      xcconfig_path = config.base_configuration_reference.real_path
      xcconfig = File.read(xcconfig_path)
      old_line = find_line_with_start(xcconfig, "OTHER_LDFLAGS")
      
      if old_line == nil
        next
      end
      new_line = ""
      new_xcconfig = xcconfig.sub(old_line, new_line)
      File.open(xcconfig_path, "w") { |file| file << new_xcconfig }
    end
  end
end
