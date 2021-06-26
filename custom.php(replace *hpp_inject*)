
if( !function_exists('flatsome_wc_get_gallery_image_html') ) {
  // Copied and modified from woocommerce plugin and wc_get_gallery_image_html helper function.

  function flatsome_wc_get_gallery_image_html( $attachment_id, $main_image = false, $size = 'woocommerce_single' ) {
    $gallery_thumbnail = wc_get_image_size( 'gallery_thumbnail' );
    $thumbnail_size    = apply_filters( 'woocommerce_gallery_thumbnail_size', array( $gallery_thumbnail['width'], $gallery_thumbnail['height'] ) );
    $image_size        = apply_filters( 'woocommerce_gallery_image_size', $size );
    $full_size         = apply_filters( 'woocommerce_gallery_full_size', apply_filters( 'woocommerce_product_thumbnails_large_size', 'full' ) );
    $thumbnail_src     = wp_get_attachment_image_src( $attachment_id, $thumbnail_size );
    $full_src          = wp_get_attachment_image_src( $attachment_id, $full_size );
    $image             = wp_get_attachment_image( $attachment_id, $image_size, false, array(
      'title'                   => get_post_field( 'post_title', $attachment_id ),
      'data-caption'            => get_post_field( 'post_excerpt', $attachment_id ),
      'data-src'                => $full_src[0],
      'data-large_image'        => $full_src[0],
      'data-large_image_width'  => $full_src[1],
      'data-large_image_height' => $full_src[2],
      'class'                   => ($main_image ? 'wp-post-image' : '').' lazy',
      'src'=> 'data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw=='
    ) );


    $image_wrapper_class = $main_image ? 'slide first' : 'slide';#_print($image);


    return '<div data-thumb="' . esc_url( $thumbnail_src[0] ) . '" class="woocommerce-product-gallery__image '.$image_wrapper_class.'"><a href="' . esc_url( $full_src[0] ) . '">' . $image . '</a></div>';
  }
}

add_filter('theme_mod_googlefonts_font_display', function(){
    return 'swap';    //optional
});

//add_action( 'wp_enqueue_scripts', function(){    wp_dequeue_script( 'webfont-loader');}, 1000);

if(0)add_action('wp_head', function(){
  //rebuild shortcode
  remove_shortcode('block');
  remove_shortcode('map');

  //block
  add_shortcode('block', function($att=[], $str=null){
    return hpp_defer_content(block_shortcode($att, $str));
  });
  
  //map
  add_shortcode('map', function($atts, $content=null, $code){
    $str = flatsome_shortcode_map($atts, $content, $code);
    $str = str_replace("google.maps.event.addDomListener(window, 'load', initialize)", "initialize();jQuery(window).resize(initialize);\n"."//google.maps.event.addDomListener(window, 'load', initialize)", $str);
    return $str;
  });
  
});

#add_filter('theme_mod_lazy_load_backgrounds', '__return_false');  //to show suddently

#add_filter('theme_mod_live_search', '__return_false');
#add_filter('theme_mod_disable_fonts', '__return_true');
add_filter('theme_mod_lazy_load_images', '__return_false');
//if disable cart
//add_filter( 'woocommerce_widget_cart_is_hidden', '__return_true' );

add_filter('flatsome_get_google_fonts_link', function($url){
  return str_replace('family=|', 'family=', urldecode($url));
});

add_filter('hpp_allow_readyjs', function($pass, $js) {
  if(hpp_in_str($js, ['window.addLoadEvent','ajaxurl = ','pagenow ='])) return false;
  return $pass;
}, 10, 2);
/*
add_filter('lightbox_content', function($txt){
  return hpp_defer_content($txt);
});

add_filter('hpp_save_merge_file', function($text, $file) {
  $text = str_replace(['b,strong{font-weight:bolder}','.nav>li>a{font-size:.8em}','.is-small,.is-small.button{font-size:.8em}'], '', $text); //old flatsome
  return $text;
}, 10, 2);
*/
add_filter('hpp_merge_file', function($code, $handle, $ext, $script_path){
  if($ext=='js' && strpos($script_path, '/flatsome.js')!==false && strpos($code,'_HWIO.')===false) 
  {
    $code = str_replace('Flatsome.behavior("sticky-sidebar",{attach:function(t){', 'Flatsome.behavior("sticky-sidebar",{attach:function(t,x1){var cb=arguments.callee;if(!x1 && !jQuery().stickySidebar) return _HWIO.waitForExist(function(){cb(t,1)},function(){return jQuery().stickySidebar},1000,100);', $code);
    if(strpos($code, '/*"use strict";*/')===false) {
      $code = str_replace('"use strict";', '/*"use strict";*/', $code);   
    }
  }
  if($ext=='js' && strpos($script_path, '/jquery.maskedinput-1.2.2.js')!==false) {
    if(strpos($code, '$.browser &&')===false) $code = str_replace('$.browser.msie ?', '$.browser && $.browser.msie ?', $code);
  }
  if($ext=='js' && strpos($script_path, '/js/smof.js')!==false) {
    if(strpos($code, 'if($.browser)if')===false) $code = str_replace('if (($.browser.msie', 'if($.browser)if (($.browser.msie', $code);
    $code = str_replace(').live(', ').on(', $code);
  }
  if($ext=='css' && strpos($script_path, '/css/flatsome.css')!==false) {
    if(strpos($code, '[data-animate]{opacity: 1')===false) $code = '[data-animate]{opacity: 1 !important;transform: none;}'. $code;
  }
  return $code;

}, 10, 4);


add_filter('hpp_merge_file', function($code, $handle, $ext, $script_path){
	if($ext=='js' && strpos($script_path, '/contact-form-7/includes/js/scripts.js')!==false) {
		$code = str_replace('$( function() {', 'setTimeout( function() {', $code);
	}
	return $code;
}, 10, 4);

if(0)add_filter('hpp_inline_script_part', function($js, $handle){
	if($handle=='contact-form-7') {
		//disable wp-json/contact-form-7/refill for boot speed
		$js = str_replace('"cached":"1"', '"cached":0', $js);
	}
	return $js;
}, 10, 2);


add_filter('hpp_merge_file', function($str, $handle, $ext, $script_path){
	if($ext=='js' && strpos($script_path,'/pum/pum-site-scripts.js')!==false){
		$search = 'var e=PUM.hooks.applyFilters("pum.initHandler",PUM.init)';
		$repl = 'var caller=arguments.callee;if(!PUM.hooks) return _HWIO.waitForExist(caller,"PUM.hooks");';

		$str = str_replace($search, $repl.$search, $str);
		$str = str_replace('r(function(){PUM.hooks.addAction("pum.integration.form.success"', 'r(function(){var caller=arguments.callee;if(!PUM.hooks) return _HWIO.waitForExist(caller,"PUM.hooks");PUM.hooks.addAction("pum.integration.form.success"', $str);
		$str = str_replace('"use strict"', '',$str);
	}
	return $str;
}, 10, 4);

add_filter('pum_generated_js', function($js){
	$search = 'var e=PUM.hooks.applyFilters("pum.initHandler",PUM.init)';
	$repl = 'var caller=arguments.callee;if(!PUM.hooks) return _HWIO.waitForExist(caller,"PUM.hooks");';
	foreach ( $js as $key => &$code ) {
		if(strpos($code['content'], $search)!==false) {
			$code['content'] = str_replace($search, $repl.$search, $code['content']);
		}
		if(strpos($code['content'], 'r(function(){PUM.hooks.addAction("pum.integration.form.success"')!==false) {
			$code['content'] = str_replace('r(function(){PUM.hooks.addAction("pum.integration.form.success"', 'r(function(){var caller=arguments.callee;if(!PUM.hooks) return _HWIO.waitForExist(caller,"PUM.hooks");PUM.hooks.addAction("pum.integration.form.success"', $code['content']);
		}
		$code['content'] = str_replace('"use strict"', '',$code['content']);
	}
	return $js;
});


add_filter('hpp_delay_asset_att', function($att, $tp) {
	if($tp=='js' ) {//&& !hw_config('merge_js')
		if($att['id']=='wc-single-product') $att['deps'].=',photoswipe';
	}
	return $att;
}, 10, 2);	

add_filter('woocommerce_queued_js', function($js){
	$js = hpp_delay_it_script( $js);
	
	return $js;
});

/*add_filter('hpp_inline_script_part', function($js, $handle){
	return $js;
}, 10, 2);*/
