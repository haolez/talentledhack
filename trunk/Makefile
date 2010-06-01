OBJS = autotalent_circular_buffer.o  autotalent_midi.o autotalent_fft.o autotalent_pitch_detector.o autotalent_formant_corrector.o autotalent_pitch_shifter.o autotalent_lfo.o autotalent_quantizer.o autotalent_lv2.o
DEBUG =
CFLAGS = --std=c99 -Wall -fPIC `pkg-config --cflags fftw3f` -O3 $(DEBUG)
LDFLAGS = $(DEBUG) `pkg-config --libs fftw3f` -shared

all: autotalent_lv2.so

autotalent_lv2.so: $(OBJS)
	ld $(LDFLAGS) $(OBJS) -o autotalent_lv2.so
cleanall: clean
	-rm *.so &>/dev/null;
clean:
	-rm *.o &>/dev/null;
	-rm dependencies/*.d &>/dev/null;
	
-include $(addprefix  dependencies/, $(OBJS:.o=.d))

%.o:%.c
	$(CC) -MMD -MP -c $(CFLAGS) $*.c -o $*.o
	mv $*.d dependencies/
install:
	echo "Copying this directory to ~/.lv2 ..."
	cp -r ../`basename \`pwd\`` ~/.lv2/
tarballs: autotalent_lv2.so
	cd ..; rm autotalent_source.tar.gz; tar -czvf autotalent_source.tar.gz autotalent.lv2/*.c autotalent.lv2/*.h autotalent.lv2/*.ttl autotalent.lv2/Makefile;
	cd ..; rm autotalent_linux_x86.tar.gz; tar -czvf autotalent_linux_x86.tar.gz autotalent.lv2/*.c autotalent.lv2/*.h autotalent.lv2/*.ttl autotalent.lv2/Makefile autotalent.lv2/autotalent_lv2.so;

.PHONY : clean cleanall install tarballs
