
cmake_minimum_required(VERSION 3.28)


set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
set(CMAKE_OSX_DEPLOYMENT_TARGET 10.15 CACHE STRING "Build for 10.15")
set(CMAKE_POSITION_INDEPENDENT_CODE ON)


project("Ripchord" VERSION 2.8.0 LANGUAGES C CXX)
include(cmake/compile-options.cmake)

add_subdirectory(libs/JUCE)

juce_add_plugin(Ripchord
  VERSION "2.8.0"
  COMPANY_NAME "Trackbout"
  COMPANY_WEBSITE "https://trackbout.com"

  FORMATS
    "VST3"
    "AU"
    "Standalone"
  PLUGIN_NAME "Ripchord"
  DESCRIPTION "Ripchord"
  PLUGIN_MANUFACTURER_CODE "TkBt"
  PLUGIN_CODE "RpCh"
  IS_SYNTH TRUE
  NEEDS_MIDI_INPUT TRUE
  NEEDS_MIDI_OUTPUT TRUE
  EDITOR_WANTS_KEYBOARD_FOCUS TRUE
  AU_MAIN_TYPE "kAudioUnitType_MIDIProcessor"
  VST3_CATEGORIES
    "Generator"
)

target_include_directories(Ripchord PUBLIC
        Source/Assets
        Source/Components
        Source/Messaging
        Source/Modules
        Source/Process
)
juce_generate_juce_header(Ripchord)

target_compile_definitions(Ripchord
  PUBLIC
    JUCE_STRICT_REFCOUNTEDPOINTER=1
    JUCE_USE_CURL=0
    JUCE_VST3_CAN_REPLACE_VST2=0
    JUCE_WEB_BROWSER=0

    JUCE_MODAL_LOOPS_PERMITTED=1
)

target_sources(Ripchord
  PRIVATE
    "Source/Components/ChordNameComponent.cpp"
    "Source/Components/DeleteComponent.cpp"
    "Source/Components/EditControlsComponent.cpp"
    "Source/Components/InputKeyboardComponent.cpp"
    "Source/Components/KeyComponent.cpp"
    "Source/Components/KeyboardComponent.cpp"
    "Source/Components/KeyboardViewComponent.cpp"
    "Source/Components/MainComponent.cpp"
    "Source/Components/MenuComponent.cpp"
    "Source/Components/OutputKeyboardComponent.cpp"
    "Source/Components/PlayControlsComponent.cpp"
    "Source/Components/PresetBrowserComponent.cpp"
    "Source/Components/PresetComponent.cpp"
    "Source/Components/PresetNameComponent.cpp"
    "Source/Components/PresetTaggerComponent.cpp"
    "Source/Components/PresetViewComponent.cpp"
    "Source/Components/RecordedMidiComponent.cpp"
    "Source/Components/RightClickComponent.cpp"
    "Source/Components/TagBarComponent.cpp"
    "Source/Components/TagBrowserComponent.cpp"
    "Source/Components/TagComponent.cpp"
    "Source/Components/TagManagerComponent.cpp"
    "Source/Messaging/DataMessage.cpp"
    "Source/Messaging/DataMessageBroadcaster.cpp"
    "Source/Messaging/DataMessageListener.cpp"
    "Source/Messaging/DataMessageManager.cpp"
    "Source/PluginEditor.cpp"
    "Source/PluginProcessor.cpp"
    "Source/Process/BrowserState.cpp"
    "Source/Process/ControlsState.cpp"
    "Source/Process/GlobalState.cpp"
    "Source/Process/MainProcess.cpp"
    "Source/Process/MidiState.cpp"
    "Source/Process/PresetState.cpp"
)

juce_add_binary_data(Ripchord_BinaryData
  SOURCES
    "Source/Assets/AllBlack.svg"
    "Source/Assets/AllBlackON.svg"
    "Source/Assets/AllWhite.svg"
    "Source/Assets/AllWhiteON.svg"
    "Source/Assets/Cancel.svg"
    "Source/Assets/CheckEmpty.svg"
    "Source/Assets/CheckFull.svg"
    "Source/Assets/CreateTag.svg"
    "Source/Assets/Delay.svg"
    "Source/Assets/DelayON.svg"
    "Source/Assets/Delete.svg"
    "Source/Assets/Direction.svg"
    "Source/Assets/DirectionAB.svg"
    "Source/Assets/DirectionABBA.svg"
    "Source/Assets/DirectionBA.svg"
    "Source/Assets/DirectionBAAB.svg"
    "Source/Assets/Down.svg"
    "Source/Assets/Favorites.svg"
    "Source/Assets/FavoritesON.svg"
    "Source/Assets/GearCircle.svg"
    "Source/Assets/KeyboardBg.svg"
    "Source/Assets/Keyboards.svg"
    "Source/Assets/MenuDuplicate.svg"
    "Source/Assets/MenuDuplicateOFF.svg"
    "Source/Assets/MenuExportMidi.svg"
    "Source/Assets/MenuExportMidiOFF.svg"
    "Source/Assets/MenuExportPreset.svg"
    "Source/Assets/MenuExportPresetOFF.svg"
    "Source/Assets/MenuImportMPC.svg"
    "Source/Assets/MenuImportMidi.svg"
    "Source/Assets/MenuImportPreset.svg"
    "Source/Assets/MenuNewPreset.svg"
    "Source/Assets/MenuThemeDARK.svg"
    "Source/Assets/MenuThemeLIGHT.svg"
    "Source/Assets/ModalBgDARK.svg"
    "Source/Assets/ModalBgLIGHT.svg"
    "Source/Assets/ModeEDIT.svg"
    "Source/Assets/ModePLAY.svg"
    "Source/Assets/MoveLeft.svg"
    "Source/Assets/MoveLeftON.svg"
    "Source/Assets/MoveRight.svg"
    "Source/Assets/MoveRightON.svg"
    "Source/Assets/NewTagBg.svg"
    "Source/Assets/Next.svg"
    "Source/Assets/NextON.svg"
    "Source/Assets/Power.svg"
    "Source/Assets/PowerON.svg"
    "Source/Assets/PresetBrowserBg.svg"
    "Source/Assets/Presets.svg"
    "Source/Assets/Prev.svg"
    "Source/Assets/PrevON.svg"
    "Source/Assets/QuickFav.svg"
    "Source/Assets/QuickFavON.svg"
    "Source/Assets/Record.svg"
    "Source/Assets/RecordIN.svg"
    "Source/Assets/RecordON.svg"
    "Source/Assets/Recorded.svg"
    "Source/Assets/RecordedIN.svg"
    "Source/Assets/RecordedON.svg"
    "Source/Assets/ResetSizeOFF.svg"
    "Source/Assets/ResetSizeON.svg"
    "Source/Assets/RightClickBgDARK.svg"
    "Source/Assets/RightClickBgLIGHT.svg"
    "Source/Assets/RightClickCopy.svg"
    "Source/Assets/RightClickCut.svg"
    "Source/Assets/RightClickPaste.svg"
    "Source/Assets/Save.svg"
    "Source/Assets/SaveON.svg"
    "Source/Assets/SearchBarBg.svg"
    "Source/Assets/ShiftLeft.svg"
    "Source/Assets/ShiftLeftON.svg"
    "Source/Assets/ShiftRight.svg"
    "Source/Assets/ShiftRightON.svg"
    "Source/Assets/Star.svg"
    "Source/Assets/StarON.svg"
    "Source/Assets/Success.svg"
    "Source/Assets/TagBarBg.svg"
    "Source/Assets/TagBrowserBg.svg"
    "Source/Assets/TagManager.svg"
    "Source/Assets/TagSelector.svg"
    "Source/Assets/TagSelectorON.svg"
    "Source/Assets/Trackbout.svg"
    "Source/Assets/Transpose.svg"
    "Source/Assets/TransposeON.svg"
    "Source/Assets/Trash.svg"
    "Source/Assets/Up.svg"
    "Source/Assets/Variance.svg"
    "Source/Assets/VarianceON.svg"
    "Source/Assets/Velocity.svg"
    "Source/Assets/VelocityON.svg"
    "Source/Assets/Version.svg"
)

target_link_libraries(Ripchord
  PRIVATE
    Ripchord_BinaryData
    juce::juce_audio_basics
    juce::juce_audio_devices
    juce::juce_audio_formats
    juce::juce_audio_plugin_client
    juce::juce_audio_processors
    juce::juce_audio_utils
    juce::juce_core
    juce::juce_cryptography
    juce::juce_data_structures
    juce::juce_events
    juce::juce_graphics
    juce::juce_gui_basics
    juce::juce_gui_extra
    juce::juce_opengl
  PUBLIC
    juce::juce_recommended_config_flags
    juce::juce_recommended_lto_flags
    juce::juce_recommended_warning_flags
)
