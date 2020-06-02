# Data format

RGB and Depth frame data are stored in matlab format files, usually named ```data_<frame_number>.mat```

The pythonic way of reading these files are

```
            data = scipy.io.loadmat(filename)['data']
            if len(data[0]) > 4:
                rgb_data = data[0][4]
            else:
                rgb_data = None
            
            phase_ampl_data = data[0][2][0][0]
```            

```phase_ampl_data``` is a ```np.uint16``` (160,120,2) array where phase is 0th dimension and amplitude is 1st dimension.

The phase data is valid in the range [0...30000] and values of 65300, 65400, 65500 denote LOW_AMPLITUDE, AMPLITUDE_SATURATION, and ADC respectively.

Valid phase can be converted to distance (cm) by using ```phase/30000*ambiguity_distance``` where ambiguity_distance is ```1.5e8/3e6*100``` for 3MHz modulation frequency.

RGB Depth camera calibration is done in a proprietary manner.
