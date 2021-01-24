project('nxp-drivers-lpc55s69', 'c',
    license : 'BSD-3-Clause',
    version : '2.2.9',
    default_options : [
        'warning_level=2',
    ],
)

c_warning_flags = meson.get_compiler('c').get_supported_arguments([
    '-Wno-unused-parameter',
])
add_project_arguments(c_warning_flags, language : 'c')

src = [
    'src/fsl_anactrl.c',
    'src/fsl_casper.c',
    'src/fsl_clock.c',
    'src/fsl_cmp.c',
    'src/fsl_common.c',
    'src/fsl_crc.c',
    'src/fsl_ctimer.c',
    'src/fsl_dma.c',
    'src/fsl_flexcomm.c',
    'src/fsl_gint.c',
    'src/fsl_gpio.c',
    'src/fsl_hashcrypt.c',
    'src/fsl_i2c.c',
    'src/fsl_i2c_dma.c',
    'src/fsl_i2s.c',
    'src/fsl_i2s_dma.c',
    'src/fsl_iap.c',
    'src/fsl_inputmux.c',
    'src/fsl_lpadc.c',
    'src/fsl_mrt.c',
    'src/fsl_ostimer.c',
    'src/fsl_pint.c',
    'src/fsl_plu.c',
    'src/fsl_power.c',
    'src/fsl_powerquad_basic.c',
    # 'src/fsl_powerquad_cmsis.c',
    'src/fsl_powerquad_data.c',
    'src/fsl_powerquad_filter.c',
    'src/fsl_powerquad_math.c',
    'src/fsl_powerquad_matrix.c',
    'src/fsl_powerquad_transform.c',
    'src/fsl_prince.c',
    'src/fsl_puf.c',
    'src/fsl_reset.c',
    'src/fsl_rng.c',
    'src/fsl_rtc.c',
    'src/fsl_sctimer.c',
    'src/fsl_sdif.c',
    'src/fsl_spi.c',
    'src/fsl_spi_dma.c',
    'src/fsl_sysctl.c',
    'src/fsl_usart.c',
    'src/fsl_usart_dma.c',
    'src/fsl_utick.c',
    'src/fsl_wwdt.c',
]

inc = include_directories('include', is_system : true)

cmsis_core_m_proj = subproject('cmsis-core-m')
cmsis_core_m_dep = cmsis_core_m_proj.get_variable('cmsis_core_m_dep')

nxp_dpal_lpc55s69_proj = subproject('nxp-dpal-lpc55s69')
nxp_dpal_lpc55s69_dep = nxp_dpal_lpc55s69_proj.get_variable('nxp_dpal_lpc55s69_dep')

if nxp_dpal_lpc55s69_dep.get_variable(internal : 'cpu_core') == 'CORE_0'
    defines = '-DCPU_LPC55S69JBD100_cm33_core0'
else
    defines = '-DCPU_LPC55S69JBD100_cm33_core1'
endif
add_project_arguments(defines, language : 'c')

nxp_drivers_lpc55s69_lib = static_library('nxp-drivers-lpc55s69', src,
    include_directories : inc,
    dependencies : [
        cmsis_core_m_dep,
        nxp_dpal_lpc55s69_dep,
    ],
    implicit_include_directories: false,
    pic: false,
)

nxp_drivers_lpc55s69_dep = declare_dependency(
    include_directories : inc,
    link_with : nxp_drivers_lpc55s69_lib,
)
