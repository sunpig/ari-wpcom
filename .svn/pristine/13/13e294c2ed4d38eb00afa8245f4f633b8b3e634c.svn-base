<?php
/**
 * Sample implementation of the Custom Header feature.
 * http://codex.wordpress.org/Custom_Headers
 *
 * @package Ari
 */

/**
 * Setup the WordPress core custom header feature.
 *
 * @uses ari_header_style()
 * @uses ari_admin_header_style()
 * @uses ari_admin_header_image()
 *
 * @package Ari
 */
function ari_custom_header_setup() {
	$options      = ari_get_theme_options();
	$header_color = 'dark' == $options['color_scheme'] ? '8a8a8a' : '88c34b';

	add_theme_support( 'custom-header', apply_filters( 'ari_custom_header_args', array(
		'default-text-color'     => $header_color,
		'width'                  => 240,
		'height'                 => 75,
		'flex-height'            => true,
		'wp-head-callback'       => 'ari_header_style',
		'admin-head-callback'    => 'ari_admin_header_style',
		'admin-preview-callback' => 'ari_admin_header_image',
	) ) );
}
add_action( 'after_setup_theme', 'ari_custom_header_setup' );

if ( ! function_exists( 'ari_header_style' ) ) :
/**
 * Styles the header image and text displayed on the blog
 *
 * @see ari_custom_header_setup().
 */
function ari_header_style() {
	?>
	<style type="text/css">
	<?php
		// Has the text been hidden?
		if ( 'blank' == get_header_textcolor() ) :
	?>
		.site-title,
		.site-description {
			position: absolute !important;
			clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
			clip: rect(1px, 1px, 1px, 1px);
		}
	<?php
		// If the user has set a custom color for the text use that
		else :
	?>
		.site-title a {
			color: #<?php echo get_header_textcolor(); ?>;
		}
	<?php endif; ?>
	</style>
	<?php
}
endif; // ari_header_style

if ( ! function_exists( 'ari_admin_header_style' ) ) :
/**
 * Styles the header image displayed on the Appearance > Header admin panel.
 *
 * @see ari_custom_header_setup().
 */
function ari_admin_header_style() {
	$options    = ari_get_theme_options();
	$text_color = $options['text_color'];

	if ( '' != get_background_color() && '' == get_background_image() )
		$background_color = get_background_color();
	else
		$background_color = 'dark' == $options['color_scheme'] ? '1b1c1b' : 'ffffff';

?>
	<style type="text/css">
	.appearance_page_custom-header #headimg {
		background-color: #<?php echo $background_color; ?>;
		border: none;
		max-width: 240px;
		padding: 10px 10px 6px 10px;
	}
	#headimg h1 {
		font-family: 'Droid Sans', Arial, sans-serif;
		font-size: 30px;
		line-height: 35px;
		margin: 0 0 5px 0;
	}
	#headimg h1 a {
		color: #<?php echo get_header_textcolor(); ?>;
		text-decoration: none;
	}
	#desc {
		color: <?php echo $text_color; ?> !important;
		font-family: 'Droid Serif', Times, serif;
		font-size: 13px;
		font-style: italic;
		line-height: 18px;
		margin: 0 0 10px 0;
	}
	</style>
<?php
}
endif; // ari_admin_header_style

if ( ! function_exists( 'ari_admin_header_image' ) ) :
/**
 * Custom header image markup displayed on the Appearance > Header admin panel.
 *
 * @see ari_custom_header_setup().
 */
function ari_admin_header_image() {
	$style        = sprintf( ' style="color:#%s;"', get_header_textcolor() );
	$header_image = get_header_image();
?>
	<div id="headimg">
		<h1 class="displaying-header-text"><a id="name"<?php echo $style; ?> onclick="return false;" href="<?php echo esc_url( home_url( '/' ) ); ?>"><?php bloginfo( 'name' ); ?></a></h1>
		<div class="displaying-header-text" id="desc"<?php echo $style; ?>><?php bloginfo( 'description' ); ?></div>
		<?php if ( ! empty( $header_image ) ) : ?>
		<img src="<?php echo esc_url( $header_image ); ?>" alt="">
		<?php endif; ?>
	</div>
<?php
}
endif; // ari_admin_header_image