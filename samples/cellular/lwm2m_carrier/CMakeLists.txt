#
# Copyright (c) 2019 Nordic Semiconductor
#
# SPDX-License-Identifier: LicenseRef-Nordic-5-Clause
#

cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(lwm2m-carrier)

# Generate hex files from pem files
set(gen_dir ${CMAKE_CURRENT_BINARY_DIR}/certs)
zephyr_include_directories(${gen_dir})
generate_inc_file_for_target(
    app
    certs/DigiCertGlobalRootCA.pem
    ${gen_dir}/DigiCertGlobalRootCA.pem.inc
    )
generate_inc_file_for_target(
    app
    certs/DigiCertGlobalRootG2.pem
    ${gen_dir}/DigiCertGlobalRootG2.pem.inc
    )
generate_inc_file_for_target(
    app
    certs/DigiCertTLSECCP384RootG5.pem
    ${gen_dir}/DigiCertTLSECCP384RootG5.pem.inc
    )
generate_inc_file_for_target(
    app
    certs/DigiCertTLSRSA4096RootG5.pem
    ${gen_dir}/DigiCertTLSRSA4096RootG5.pem.inc
    )
generate_inc_file_for_target(
    app
    certs/DigiCertTrustedRootG4.pem
    ${gen_dir}/DigiCertTrustedRootG4.pem.inc
    )

# NORDIC SDK APP START
target_sources(app PRIVATE src/main.c)
target_sources(app PRIVATE src/carrier_certs.c)
# NORDIC SDK APP END
