vkd3d_shaders =[
  'shaders/cs_clear_uav_buffer_float.comp',
  'shaders/cs_clear_uav_buffer_raw.comp',
  'shaders/cs_clear_uav_buffer_uint.comp',
  'shaders/cs_clear_uav_image_1d_array_float.comp',
  'shaders/cs_clear_uav_image_1d_array_uint.comp',
  'shaders/cs_clear_uav_image_1d_float.comp',
  'shaders/cs_clear_uav_image_1d_uint.comp',
  'shaders/cs_clear_uav_image_2d_array_float.comp',
  'shaders/cs_clear_uav_image_2d_array_uint.comp',
  'shaders/cs_clear_uav_image_2d_float.comp',
  'shaders/cs_clear_uav_image_2d_uint.comp',
  'shaders/cs_clear_uav_image_3d_float.comp',
  'shaders/cs_clear_uav_image_3d_uint.comp',
  'shaders/cs_predicate_command.comp',
  'shaders/cs_resolve_binary_queries.comp',
  'shaders/cs_resolve_predicate.comp',
  'shaders/cs_resolve_query.comp',

  'shaders/fs_copy_image_float.frag',
  'shaders/fs_copy_image_uint.frag',
  'shaders/fs_copy_image_stencil.frag',

  'shaders/gs_fullscreen.geom',
  'shaders/vs_fullscreen.vert',
  'shaders/vs_fullscreen_layer.vert',

  'shaders/vs_swapchain_fullscreen.vert',
  'shaders/fs_swapchain_fullscreen.frag',
  'shaders/cs_execute_indirect_patch.comp',
  'shaders/cs_execute_indirect_patch_debug_ring.comp',
  'shaders/cs_execute_indirect_multi_dispatch.comp',
  'shaders/cs_execute_indirect_multi_dispatch_state.comp',
]

vkd3d_src = [
  'bundle.c',
  'cache.c',
  'command.c',
  'command_list_vkd3d_ext.c',
  'device.c',
  'device_vkd3d_ext.c',
  'heap.c',
  'memory.c',
  'meta.c',
  'resource.c',
  'state.c',
  'utils.c',
  'debug_ring.c',
  'va_map.c',
  'vkd3d_main.c',
  'raytracing_pipeline.c',
  'acceleration_structure.c',
  'swapchain.c'
]

if enable_renderdoc
  vkd3d_src += ['renderdoc.c']
endif

if enable_descriptor_qa
  vkd3d_src += ['descriptor_debug.c']
endif

if enable_breadcrumbs
  vkd3d_src += ['breadcrumbs.c']
endif

if vkd3d_platform == 'windows'
  vkd3d_src += ['shared_metadata.c']
endif

vkd3d_lib = static_library('vkd3d-proton', vkd3d_src, glsl_generator.process(vkd3d_shaders), vkd3d_build, vkd3d_version,
  dependencies        : [ vkd3d_common_dep, vkd3d_shader_dep ] + vkd3d_extra_libs,
  include_directories : vkd3d_private_includes,
  override_options    : [ 'c_std='+vkd3d_c_std ])

vkd3d_dep = declare_dependency(
  link_with           : [ vkd3d_lib, vkd3d_common_lib ],
  dependencies        : [ vkd3d_extra_libs, vkd3d_common_dep ],
  include_directories : vkd3d_public_includes)
