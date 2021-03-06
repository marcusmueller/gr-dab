# Copyright 2011,2012 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Setup library
########################################################################
include(GrPlatform) #define LIB_SUFFIX

include_directories(${Boost_INCLUDE_DIR} ${FDK-AAC_INCLUDE_DIRS} ${LIBTOOLAME-DAB_INCLUDE_DIR})
link_directories(${Boost_LIBRARY_DIRS})
list(APPEND dab_sources
    moving_sum_ff_impl.cc
    ofdm_ffe_all_in_one_impl.cc
    ofdm_sampler_impl.cc
    ofdm_coarse_frequency_correct_impl.cc
    diff_phasor_vcc_impl.cc
    ofdm_remove_first_symbol_vcc_impl.cc
    frequency_interleaver_vcc_impl.cc
    qpsk_demapper_vcb_impl.cc
    complex_to_interleaved_float_vcf_impl.cc
    modulo_ff_impl.cc
    measure_processing_rate_impl.cc
    select_vectors_impl.cc
    repartition_vectors_impl.cc
    unpuncture_vff_impl.cc
    prune_vectors_impl.cc
    fib_sink_vb_impl.cc
    crc16.cc
    estimate_sample_rate_bf_impl.cc
    fractional_interpolator_triggered_update_cc_impl.cc
    magnitude_equalizer_vcc_impl.cc
    qpsk_mapper_vbc_impl.cc
    ofdm_insert_pilot_vcc_impl.cc
    sum_phasor_trig_vcc_impl.cc
    ofdm_move_and_insert_zero_impl.cc
    insert_null_symbol_impl.cc
    time_interleave_bb_impl.cc
    time_deinterleave_ff_impl.cc
    crc16_bb_impl.cc
    fib_source_b_impl.cc
    select_subch_vfvf_impl.cc
    unpuncture_ff_impl.cc
    prune_impl.cc
    firecode-checker.cpp
    firecode_check_bb_impl.cc
    puncture_bb_impl.cc
    dab_transmission_frame_mux_bb_impl.cc
    conv_encoder_bb_impl.cc
    mapper_bc_impl.cc
    mp2_decode_bs_impl.cc
    mp4_decode_bs_impl.cc
    reed_solomon_decode_bb_impl.cc
    fec/decode_rs_char.c
    fec/encode_rs_char.c
    fec/init_rs_char.c
    reed_solomon_encode_bb_impl.cc
    mp4_encode_sb_impl.cc
    mp2_encode_sb_impl.cc
    ${LIBTOOLAME-DAB_SOURCE_DIR}/ath.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/crc.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/fft.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/mem.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/utils.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/common.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/encode.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/tables.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/subband.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/toolame.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/psycho_0.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/psycho_1.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/psycho_2.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/psycho_3.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/psycho_4.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/availbits.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/bitstream.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/ieeefloat.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/psycho_n1.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/encode_new.c
    ${LIBTOOLAME-DAB_SOURCE_DIR}/portableio.c
)


set(dab_sources "${dab_sources}" PARENT_SCOPE)
if(NOT dab_sources)
	MESSAGE(STATUS "No C++ sources... skipping lib/")
	return()
endif(NOT dab_sources)

add_library(gnuradio-dab SHARED ${dab_sources})
target_link_libraries(gnuradio-dab ${Boost_LIBRARIES} ${GNURADIO_ALL_LIBRARIES} ${GNURADIO_FILTER_LIBRARIES} ${FAAD_LIBRARIES} ${FDK-AAC_LIBRARIES})
set_target_properties(gnuradio-dab PROPERTIES DEFINE_SYMBOL "gnuradio_dab_EXPORTS")

if(APPLE)
    set_target_properties(gnuradio-dab PROPERTIES
        INSTALL_NAME_DIR "${CMAKE_INSTALL_PREFIX}/lib"
    )
endif(APPLE)

########################################################################
# Install built library files
########################################################################
install(TARGETS gnuradio-dab
    LIBRARY DESTINATION lib${LIB_SUFFIX} # .so/.dylib file
    ARCHIVE DESTINATION lib${LIB_SUFFIX} # .lib file
    RUNTIME DESTINATION bin              # .dll file
)

########################################################################
# Build and register unit test
########################################################################
include(GrTest)

include_directories(${CPPUNIT_INCLUDE_DIRS})

list(APPEND test_dab_sources
    ${CMAKE_CURRENT_SOURCE_DIR}/test_dab.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/qa_dab.cc
)

add_executable(test-dab ${test_dab_sources})


target_link_libraries(
  test-dab
  ${GNURADIO_RUNTIME_LIBRARIES}
  ${GNURADIO_FILTER_LIBRARIES}
  ${Boost_LIBRARIES}
  ${CPPUNIT_LIBRARIES}
  gnuradio-dab
)

GR_ADD_TEST(test_dab test-dab)
