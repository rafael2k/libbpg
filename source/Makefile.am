AM_CFLAGS   = -Wall -Wextra -Wno-sign-compare -Wno-unused-parameter -Wno-unused-but-set-variable
AM_CPPFLAGS = -DCONFIG_BPG_VERSION=\"@VERSION@\"
AM_CXXFLAGS = $(AM_CFLAGS)



bin_PROGRAMS    = bpgdec bpgenc bpgmux bpgview
lib_LTLIBRARIES = libbpg.la
include_HEADERS = libbpg.h



libbpg_la_SOURCES = \
		libavcodec/hevc_cabac.c \
		libavcodec/hevc_filter.c \
		libavcodec/hevc.c \
		libavcodec/hevcpred.c \
		libavcodec/hevc_refs.c \
		libavcodec/hevcdsp.c \
		libavcodec/hevc_mvs.c \
		libavcodec/hevc_ps.c \
		libavcodec/hevc_sei.c \
		libavcodec/utils.c \
		libavcodec/cabac.c \
		libavcodec/golomb.c \
		libavcodec/videodsp.c \
		libavutil/mem.c \
		libavutil/buffer.c \
		libavutil/log2_tab.c \
		libavutil/frame.c \
		libavutil/pixdesc.c \
		libavutil/md5.c \
		libbpg.c
libbpg_la_CFLAGS   = $(AM_CFLAGS) -Ilibavcodec
libbpg_la_CPPFLAGS = $(AM_CPPFLAGS) \
		-D_ISOC99_SOURCE -D_POSIX_C_SOURCE=200112 -D_XOPEN_SOURCE=600 \
		-DHAVE_AV_CONFIG_H -std=c99 -D_GNU_SOURCE=1 -DUSE_VAR_BIT_DEPTH -DUSE_PRED

# name the shared library libbpg-VERSION.so.0 until the first official
# libbpg.so.0 version is released
libbpg_la_LDFLAGS = -release $(VERSION) -version-info 0:0:0 -Wl,--version-script=$(srcdir)/libbpg.map



bpgdec_SOURCES = bpgdec.c
bpgdec_LDADD   = libbpg.la $(PNG16_LIBS) -lz



bpgenc_SOURCES  = bpgenc.c
bpgenc_CFLAGS   = $(AM_CFLAGS) $(PNG16_CFLAGS)
bpgenc_CPPFLAGS = $(AM_CPPFLAGS)
bpgenc_CXXFLAGS = $(AM_CXXFLAGS)
bpgenc_LDADD    = libbpg.la $(PNG16_LIBS) -lz

if USE_JCTVC
bpgenc_SOURCES += jctvc_glue.cpp \
		jctvc/TLibVideoIO/TVideoIOYuv.cpp \
		jctvc/program_options_lite.cpp \
		jctvc/TLibEncoder/SyntaxElementWriter.cpp \
		jctvc/TLibEncoder/TEncSearch.cpp \
		jctvc/TLibEncoder/TEncGOP.cpp \
		jctvc/TLibEncoder/TEncTop.cpp \
		jctvc/TLibEncoder/TEncBinCoderCABACCounter.cpp \
		jctvc/TLibEncoder/TEncCavlc.cpp \
		jctvc/TLibEncoder/TEncCu.cpp \
		jctvc/TLibEncoder/TEncSlice.cpp \
		jctvc/TLibEncoder/TEncPic.cpp \
		jctvc/TLibEncoder/TEncSampleAdaptiveOffset.cpp \
		jctvc/TLibEncoder/WeightPredAnalysis.cpp \
		jctvc/TLibEncoder/TEncBinCoderCABAC.cpp \
		jctvc/TLibEncoder/SEIwrite.cpp \
		jctvc/TLibEncoder/TEncRateCtrl.cpp \
		jctvc/TLibEncoder/TEncPreanalyzer.cpp \
		jctvc/TLibEncoder/NALwrite.cpp \
		jctvc/TLibEncoder/SEIEncoder.cpp \
		jctvc/TLibEncoder/TEncSbac.cpp \
		jctvc/TLibEncoder/TEncEntropy.cpp \
		jctvc/TLibCommon/TComWeightPrediction.cpp \
		jctvc/TLibCommon/TComPattern.cpp \
		jctvc/TLibCommon/TComSampleAdaptiveOffset.cpp \
		jctvc/TLibCommon/TComPicSym.cpp \
		jctvc/TLibCommon/TComPicYuvMD5.cpp \
		jctvc/TLibCommon/SEI.cpp \
		jctvc/TLibCommon/ContextModel3DBuffer.cpp \
		jctvc/TLibCommon/Debug.cpp \
		jctvc/TLibCommon/TComPicYuv.cpp \
		jctvc/TLibCommon/TComInterpolationFilter.cpp \
		jctvc/TLibCommon/TComTrQuant.cpp \
		jctvc/TLibCommon/TComRdCostWeightPrediction.cpp \
		jctvc/TLibCommon/TComLoopFilter.cpp \
		jctvc/TLibCommon/TComChromaFormat.cpp \
		jctvc/TLibCommon/TComSlice.cpp \
		jctvc/TLibCommon/TComDataCU.cpp \
		jctvc/TLibCommon/TComTU.cpp \
		jctvc/TLibCommon/TComCABACTables.cpp \
		jctvc/TLibCommon/TComPic.cpp \
		jctvc/TLibCommon/TComRom.cpp \
		jctvc/TLibCommon/TComYuv.cpp \
		jctvc/TLibCommon/TComPrediction.cpp \
		jctvc/TLibCommon/TComMotionInfo.cpp \
		jctvc/TLibCommon/TComBitStream.cpp \
		jctvc/TLibCommon/ContextModel.cpp \
		jctvc/TLibCommon/TComRdCost.cpp \
		jctvc/TAppEncTop.cpp \
		jctvc/TAppEncCfg.cpp \
		jctvc/libmd5/libmd5.c
bpgenc_CPPFLAGS += -DUSE_JCTVC
bpgenc_CXXFLAGS += -Ijctvc
endif

if USE_X265
bpgenc_SOURCES  += x265_glue.c
bpgenc_CPPFLAGS += -DUSE_X265
bpgenc_LDADD    += -lx265
endif



bpgview_SOURCES = bpgview.c
bpgview_LDADD   = libbpg.la $(SDL_LIBS) $(SDL_IMAGE_LIBS)



bpgmux_SOURCES = bpgmux.c bpgfmt.c



JAVASCRIPTS =
EMCFLAGS :=
if USE_EMCC
JAVASCRIPTS += bpgdec.js bpgdec8.js bpgdec8a.js
CLEANFILES   = $(JAVASCRIPTS)

EMCFLAGS += -Wall -Wno-unused-function -Wno-unused-variable -I. -I.. $(AM_CPPFLAGS)
EMCFLAGS += -DHAVE_CONFIG_H
EMCFLAGS += -D_ISOC99_SOURCE -D_POSIX_C_SOURCE=200112 -D_XOPEN_SOURCE=600 -DHAVE_AV_CONFIG_H -std=c99 -D_GNU_SOURCE=1

EMLDFLAGS := -s "EXPORTED_FUNCTIONS=['_bpg_decoder_open','_bpg_decoder_decode','_bpg_decoder_get_info','_bpg_decoder_start','_bpg_decoder_get_frame_duration','_bpg_decoder_get_line','_bpg_decoder_close','_malloc','_free']"
EMLDFLAGS += -s NO_FILESYSTEM=1 -s NO_BROWSER=1
EMLDFLAGS += -O3 --memory-init-file 0 --closure 1 --post-js post.js

LIBBPG_JS_OBJS   = $(patsubst %.c, %.js.o, $(libbpg_la_SOURCES)) tmalloc.js.o
LIBBPG_JS8_OBJS  = $(patsubst %.c, %.js8.o, $(libbpg_la_SOURCES)) tmalloc.js8.o
LIBBPG_JS8A_OBJS = $(patsubst %.c, %.js8a.o, $(libbpg_la_SOURCES)) tmalloc.js8a.o

$(LIBBPG_JS_OBJS): EMCFLAGS+=-DUSE_VAR_BIT_DEPTH
$(LIBBPG_JS8_OBJS): EMCFLAGS+=
$(LIBBPG_JS8A_OBJS): EMCFLAGS+=-DUSE_PRED

bpgdec.js: $(LIBBPG_JS_OBJS)
	$(EMCC) $(EMLDFLAGS) -s TOTAL_MEMORY=33554432 -o $@ $(LIBBPG_JS_OBJS)

bpgdec8.js: $(LIBBPG_JS8_OBJS)
	$(EMCC) $(EMLDFLAGS) -s TOTAL_MEMORY=16777216 -o $@ $(LIBBPG_JS8_OBJS)

bpgdec8a.js: $(LIBBPG_JS8A_OBJS)
	$(EMCC) $(EMLDFLAGS) -s TOTAL_MEMORY=16777216 -o $@ $(LIBBPG_JS8A_OBJS)

%.js.o: %.c
	$(EMCC) $(EMCFLAGS) -c -o $@ $<

%.js8.o: %.c
	$(EMCC) $(EMCFLAGS) -c -o $@ $<

%.js8a.o: %.c
	$(EMCC) $(EMCFLAGS) -c -o $@ $<
endif



# hack libbpg.la to install the library as libbpg-VERSION.so.0 and create the following
# symbolic links to it: libbpg-VERSION.so libbpg.so
all-local: javascripts
	[ ! -f libbpg.la ] || sed -i "s/library_names='libbpg-$(VERSION).so.0.0.0 libbpg-$(VERSION).so.0 libbpg.so'/library_names='libbpg-$(VERSION).so.0 libbpg-$(VERSION).so libbpg.so'/" libbpg.la

javascripts: $(JAVASCRIPTS)



# remove '-ljpeg' from the dependency line inside libbpg.la since
# the library doesn't actually depend on it (temporary solution)
install-exec-hook:
	[ ! -f $(DESTDIR)$(libdir)/libbpg.la ] || sed -i 's/-ljpeg//' $(DESTDIR)$(libdir)/libbpg.la


