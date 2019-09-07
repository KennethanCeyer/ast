<h1 align="center">AST</h1>

<p align="center">Advanced Sound Tool :sound:</p>

## Notice

This project is in progress for developing, If you like this project's purpose
Please star it to express your passionated rejoicing! :smile:

## What is AST?

Ast is an advanced sound tool, This tool is made for conversion the audio rate, bit depth and format.

The tool supports both command line and library methods, These day Golang audio eco system is too undeveloped, This is why the project is in progress for developing.

## Okay, So what is features which this library is supported?

### Conversion

#### Format change

```go
audio := NewAudio("./my_audio.wav")
newAudio := audio.To(codec.Mp3)

// save to your local disk
newAudio.Save("./my_new_audio.mp3")

// get the raw bytes
data := newAudio.Bytes()
```

#### Sampling

```go
audio := NewAudio("./my_audio.wav")
newAudio := audio.To(codec.Mp3).Convert(&codec.Format{
	SampleRate: 8000,
	BitDepth: 16,
	Channel: codec.MonoChannel,
})

// save to your local disk
newAudio.Save("./my_new_audio.mp3")

// get the raw bytes
data := newAudio.Bytes()
```

```go
audio := NewAudio("./my_audio.raw").WithType(&codec.Format{
	Encode: codec.Linear16Encode,
	SampleRate: 8000,
	BitDepth: 16,
	Channel: codec.MonoChannel,
})
newAudio := audio.To(codec.Mp3).Convert(&codec.Format{
    SapleRate: 16000,
    BitDepth: 16,
    Channel: codec.MonoChannel,
})

// save to your local disk
newAudio.Save("./my_new_audio.mp3")

// get the raw bytes
data := newAudio.Bytes()
```

### Analyze

```go
audio := NewAudio("./my_audio.wav")
log.Println(audio.Analyze())
```

**OUTPUT**
```plaintext
FileType: Wav
IsValid: true
ChunkSize: 8192
Chnanel: Mono(1)
SampleRate: 8000
BitDepth: 8
NumSamples: 1824
```

There are quick and fast feature to get attribute for each format
```go
pcm := audio.GetPCM()
spectrum := audio.Spectrum()
spectrum.Save("./my_spectrum.png")
```

### Audio Toolkit

Manipulate audio data with a simple method

```go
audio := NewAudio("./my_audio.wav")

audio.Speed(1.2) // 120% faster
audio.Pitch(1.15) // Up to 1.15 high pitch
audio.Alpha(0.9) // Low as 90% tone

audio.LowPassFilter()
audio.Save("./my_new_audio.wav")
```

Merge two audio

```go
audio := NewAudio("./my_audio.wav")
backgroundAudio := NewAudio("./my_background.mp3")

audio.Merge(backgroundAudio)
audio.Save("./my_new_audio.wav")
```

Concatenate two audios

```go
audio := NewAudio("./my_audio.wav")
backgroundAudio := NewAudio("./my_background.mp3")

audio.Concat(backgroundAudio)
audio.Save("./my_new_audio.wav")
```

### Road map

#### Audio Format

- PCM
    - Linear16
    - G711 A Type
    - G711 U Type
    
- Wav
- Mpeg
    - Mp3
    - Mp4
- Speex
- Flac

#### Features

**Sampling**

- UpSample / DownSample
- BitDepth Conversion
- Channel Conversion
- Interpolation (Cubic, Linear)
- Filter

**Format Conversion**

**Audio Controlling**

- Pitch control
- Alpha control
- Speed control
- Cutting audio
- Merge audio
- Concat audio 
