env start

conda activate MCS_25   

info

ffprobe amused_1-15_0001.wav

delka?

soxi -T -D *.wav

prekodovani na pcm_s16le

ffmpeg -i amused_1-15_0001.wav -c:a pcm_s16le output-16.wav

bitrate set to 8khz
ffmpeg -i output-16.wav -ar 8000 output-16-8khz.wav


//doesnt work -gsm/libgsm
ffmpeg -i output-16-8khz.wav -c:a libgsm output-16-8khz-gsm.wav

//alternative
ffmpeg -i output-16-8khz.wav -ar 8000 -ac 1 -c:a libopencore_amrnb output-16-8khz-amr.wav

//ar sample rate 8k         b:a  bitrate 12k

ffmpeg -i output-16-8khz.wav -ar 8000 -c:a libopus -b:a 12k output-opus.opus 

ffmpeg -i output-opus.opus -ar 8k output-opus.wav 


ffmpeg -i output-16-8khz.wav -c:a aac -b:a 12k output-aac.aac


