# Video Call Stand-In

An interactive audio visualizer with profile picture display - perfect for video call participants who want to share something more engaging than a blank screen when they don't have video enabled.

## Features

- **Real-time Audio Visualization**: Display your microphone input with beautiful visualizations
  - Circular frequency bars (radial equalizer)
  - Waveform oscilloscope
  - Particle effects
  - Pulsing rings

- **Profile Picture**: Upload and display a circular profile photo in the center
  - Automatic square cropping
  - Saved to browser localStorage (persists across sessions)
  - Easy remove option

- **Hidden Controls**: Clean interface with auto-hiding controls
  - Show on mouse movement or any keypress
  - Auto-hide after 3 seconds of inactivity
  - Cursor automatically hides for clean screen sharing

- **Customization Options**:
  - Adjustable sensitivity for different microphone levels
  - Smoothing control for visualization fluidity
  - Color picker for personalized themes
  - Toggle microphone on/off

## Usage

### Quick Start

1. Open `index.html` in a modern web browser (Chrome, Firefox, Edge, Safari)
2. Allow microphone access when prompted
3. Move your mouse or press any key to show controls
4. Upload a profile picture (optional)
5. Adjust settings to your preference
6. Share your screen in your video call!

### Screen Sharing Tips

1. **Browser Tab Sharing**: Share just the browser tab (most efficient)
2. **Fullscreen Mode**: Press F11 for fullscreen before sharing
3. **Hide Controls**: Let controls auto-hide before sharing your screen
4. **Test Audio**: Speak to see the visualization respond to your voice

### Controls

- **Profile Picture**: Upload a photo that will be displayed in the center
- **Visualization Style**: Choose between different animation styles
- **Sensitivity**: Adjust how responsive the visualization is to audio (10-200%)
- **Smoothing**: Control how fluid the animations are (0-100%)
- **Visualization Color**: Pick your preferred color theme
- **Microphone Toggle**: Turn audio visualization on/off

## Browser Compatibility

Works in all modern browsers that support:
- Web Audio API
- Canvas API
- localStorage
- getUserMedia (microphone access)

Tested on:
- Chrome 90+
- Firefox 88+
- Edge 90+
- Safari 14+

## Privacy

- All data stays in your browser
- Profile pictures are stored in browser localStorage only
- No data is sent to any server
- Microphone audio is processed locally and never recorded

## Keyboard Shortcuts

- Any key: Show controls
- F11: Toggle fullscreen (browser default)

## Technical Details

Built with vanilla JavaScript, no dependencies required. Uses:
- Web Audio API for microphone input and frequency analysis
- Canvas API for smooth 60fps visualizations
- localStorage for persistent profile picture
- CSS3 for modern UI with backdrop filters

## Troubleshooting

**Microphone not working?**
- Check browser permissions for microphone access
- Make sure microphone is not muted in system settings
- Try refreshing the page

**Visualization not responding?**
- Increase the sensitivity slider
- Check if microphone toggle is ON
- Speak louder or closer to your microphone

**Controls won't hide?**
- Move your mouse outside the control panel area
- Wait 3 seconds without mouse movement

## License

MIT License - feel free to use, modify, and share!