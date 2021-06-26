
$('[data-animate]').removeAttr('data-animate');
$('.slider-wrapper').attr('style','max-height:initial !important;')
_HWIO.waitForExist(function(){
$("[data-countdown]").each(function(){var t=$(this),s=$(this).data("countdown"),n=$(this).data("text-hour"),a=$(this).data("text-min"),e=$(this).data("text-week"),r=jQuery(this).data("text-day"),o=jQuery(this).data("text-sec"),u=jQuery(this).data("text-min-p"),d=jQuery(this).data("text-hour-p"),i=jQuery(this).data("text-week-p"),p=jQuery(this).data("text-day-p"),h=jQuery(this).data("text-sec-p"),y=jQuery(this).data("text-plural"),g=n+y,j=r+y,Q=e+y,c=a,x=o;d&&(g=d),u&&(c=u),i&&(Q=i),p&&(j=p),h&&(x=h),t.countdown(s).on("update.countdown",function(t){var s="<span>%-H<strong>%!H:"+n+","+g+";</strong></span><span>%-M<strong>%!M:"+a+","+c+";</strong></span><span>%-S<strong>%!S:"+o+","+x+";</strong></span>";0<t.offset.days&&(s="<span>%-d<strong>%!d:"+r+","+j+";</strong></span>"+s),0<t.offset.weeks&&(s="<span>%-w<strong>%!w:"+e+","+Q+";</strong></span>"+s),jQuery(this).html(t.strftime(s))}).on("finish.countdown",function(t){var s="<span>%-H<strong>%!H:"+n+","+g+";</strong></span><span>%-M<strong>%!M:"+a+","+c+";</strong></span><span>%-S<strong>%!S:"+o+","+x+";</strong></span>";jQuery(this).html(t.strftime(s))})});
},function(){return $().countdown;});



function initContactForm() {
    if(initContactForm.init || typeof wpcf7=='undefined' || typeof wpcf7.initForm=='undefined') return;
    //adjust by you
    if($( 'div.wpcf7,.wpcf7-form' ).length) initContactForm.init=1;else return;
    console.log('init form');
    $( 'div.wpcf7 > form,.wpcf7-form' ).each( function() {
        var $form = $( this );
        wpcf7.initForm( $form );
        if ( wpcf7.cached ) {
            wpcf7.refill( $form );
        }
    } );
}
_HWIO.readyjs(function(){
	if(typeof wpcf7=='undefined') return;
	initContactForm();
	document.dispatchEvent(new Event("DOMContentLoaded"));
	document.dispatchEvent(new Event("wpcf7grecaptchaexecuted"));
});


$('.woocommerce-product-gallery').css({'overflow':'', 'max-height':''});
	
