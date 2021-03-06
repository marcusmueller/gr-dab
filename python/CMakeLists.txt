# Copyright 2011 Free Software Foundation, Inc.
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
# Include python install macros
########################################################################
include(GrPython)
if(NOT PYTHONINTERP_FOUND)
    return()
endif()

########################################################################
# Install python sources
########################################################################
GR_PYTHON_INSTALL(
    FILES
    __init__.py
    ofdm_sync_dab.py
    ofdm_sync_dab2.py
    detect_null.py
    ofdm.py
    parameters.py
    fic.py
    msc_decode.py
    fic_encode.py
    msc_encode.py
    transmitter_c.py
    dabplus_audio_decoder_ff.py DESTINATION ${GR_PYTHON_DIR}/dab
)

########################################################################
# Handle the unit tests
########################################################################
include(GrTest)

set(GR_TEST_TARGET_DEPS gnuradio-dab)
set(GR_TEST_PYTHON_DIRS ${CMAKE_BINARY_DIR}/swig)
GR_ADD_TEST(qa_time_interleave_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_time_interleave_bb.py)
GR_ADD_TEST(qa_time_deinterleave_ff ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_time_deinterleave_ff.py)
GR_ADD_TEST(qa_fib_sink_vb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_fib_sink_vb.py)
GR_ADD_TEST(qa_crc16_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_crc16_bb.py)
GR_ADD_TEST(qa_fib_source_b ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_fib_source_b.py)
GR_ADD_TEST(qa_select_subch_vfvf ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_select_subch_vfvf.py)
GR_ADD_TEST(qa_unpuncture_ff ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_unpuncture_ff.py)
GR_ADD_TEST(qa_prune ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_prune.py)
GR_ADD_TEST(qa_fic_encode ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_fic_encode.py)
GR_ADD_TEST(qa_puncture_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_puncture_bb.py)
GR_ADD_TEST(qa_msc_encode ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_msc_encode.py)
GR_ADD_TEST(qa_dab_transmission_frame_mux_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_dab_transmission_frame_mux_bb.py)
GR_ADD_TEST(qa_conv_encoder_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_conv_encoder_bb.py)
GR_ADD_TEST(qa_mapper_bc ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_mapper_bc.py)
GR_ADD_TEST(qa_mp2_decode_bs ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_mp2_decode_bs.py)
GR_ADD_TEST(qa_mp4_decode_bs ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_mp4_decode_bs.py)
GR_ADD_TEST(qa_dabplus_audio_decoder_ff ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_dabplus_audio_decoder_ff.py)
GR_ADD_TEST(qa_reed_solomon_decode_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_reed_solomon_decode_bb.py)
GR_ADD_TEST(qa_reed_solomon_encode_bb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_reed_solomon_encode_bb.py)
GR_ADD_TEST(qa_mp4_encode_sb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_mp4_encode_sb.py)
GR_ADD_TEST(qa_mp2_encode_sb ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_mp2_encode_sb.py)
