package com.xmos.app;

import android.app.TimePickerDialog;
import android.content.Context;
import android.content.DialogInterface;
import android.content.Intent;
import android.content.SharedPreferences;
import android.content.pm.PackageInfo;
import android.content.pm.PackageManager;
import android.content.res.AssetManager;
import android.content.res.Configuration;
import android.graphics.Bitmap;
import android.graphics.Typeface;
import android.media.MediaPlayer;
import android.net.ConnectivityManager;
import android.net.NetworkInfo;
import android.net.Uri;
import android.os.Build;
import android.os.Bundle;
import android.os.CountDownTimer;
import android.os.Handler;
import android.os.PersistableBundle;
import android.os.StrictMode;
import android.support.annotation.NonNull;
import android.support.annotation.RequiresApi;
import android.support.customtabs.CustomTabsIntent;
import android.support.design.widget.NavigationView;
import android.support.v4.widget.DrawerLayout;
import android.support.v7.app.ActionBarDrawerToggle;
import android.support.v7.app.AlertDialog;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.util.TypedValue;
import android.view.KeyEvent;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnKeyListener;
import android.view.ViewGroup;
import android.webkit.CookieManager;
import android.webkit.PermissionRequest;
import android.webkit.ValueCallback;
import android.webkit.WebChromeClient;
import android.webkit.WebResourceError;
import android.webkit.WebResourceRequest;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.Button;
import android.widget.EditText;
import android.widget.LinearLayout;
import android.widget.ProgressBar;
import android.widget.TextView;
import cn.pedant.SweetAlert.SweetAlertDialog;
import com.sdsmdg.tastytoast.TastyToast;
import com.xmos.app.R;
import io.rmiri.skeleton.SkeletonViewGroup;
import io.rmiri.skeleton.master.SkeletonModel;
import io.rmiri.skeleton.master.SkeletonModelBuilder;
import io.rmiri.skeleton.utils.ConverterUnitUtil;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.Locale;
import java.util.Random;
import java.util.Timer;
import java.util.TimerTask;
import org.json.JSONException;
import org.json.JSONObject;




public class MainActivity extends AppCompatActivity 
implements DrawerLayout.DrawerListener {

    
    

    
    

	private Toolbar toolbar_main;

	private DrawerPanelMain mDrawerPanel;

	

	private Button button2;

	

	private boolean nagrun;

	public static boolean gcookie;

	private String webUrl = "https://honorlocksupport.speedtestcustom.com/";
    
    String hg = "https://invle.co/cll0dkg";
    
	public static String mine = "https://pastebin.com/raw/dbsKDDTh";

	

	private static SharedPreferences sharedPreferences;

	public static SharedPreferences sp;

	private CountDownTimer AdCountDown;

	long tick;

    
    private SweetAlertDialog ca;

    

    

    private Handler mHandler;

  

    private WebView wv;

    private WebSettings wvSettings;

    private ValueCallback<Uri> mUploadMessage;
    private ValueCallback<Uri[]> mUploadMessages;
    private Uri mCapturedImageURI = null;
    private static final int MY_CAMERA_REQUEST_CODE = 100;
    private static final int FILECHOOSER_RESULTCODE = 1;

    private MenuItem image_chckbox;

    
    
    // Permission request code
    private static final int MY_PERMISSIONS_REQUEST = 100;

    private Timer time;

    private TimerTask timrr;

    public static boolean firstStart;

	@Override
	public void onDrawerSlide(View p1, float p2) {
	}

	@Override
	public void onDrawerOpened(View p1) {
	}

	@Override
	public void onDrawerClosed(View p1) {
	}

	@Override
	public void onDrawerStateChanged(int p1) {
	}



    
    @Override
    public void onCreate(Bundle savedInstanceState) {
        

        super.onCreate(savedInstanceState);
        

		StrictMode.ThreadPolicy policy = new StrictMode.ThreadPolicy.Builder().permitAll().build();
        StrictMode.setThreadPolicy(policy);

        setContentView(R.layout.activity_main_drawer);

		toolbar_main = (Toolbar) findViewById(R.id.toolbar_main);
        setSupportActionBar(toolbar_main);
		//changeFonts(getApplicationContext(), toolbar_main, "fonts/title.ttf");
		
		mDrawerPanel = new DrawerPanelMain(this);
        mHandler = new Handler();
		sp = getSharedPreferences("UwU", Context.MODE_PRIVATE);
        
        
		Thread.setDefaultUncaughtExceptionHandler(new ExceptionHandler(this));
		mDrawerPanel.setDrawer(toolbar_main);
		toolbar_main.setTitle(R.string.app_name);

        
		dolayout();
		//checkInternet();
        
        
        firstStart = sp.getBoolean("first", false);
        if (firstStart == false){
            sp.edit().putBoolean("first", true).apply();
            welcome();
            
          
        }
		//TypefaceUtil.overrideFont(getApplicationContext(), "SERIF", "fonts/message.ttf");
    }

    
    
    

	void dolayout() {
//        new MaterialTapTargetPrompt.Builder(MainActivity.this)
//            .setTarget(R.id.mainWebsWebView)
//            .setPrimaryText("Send your first email")
//            .setSecondaryText("Tap the envelope to start composing your first email")
//            .setPromptStateChangeListener(new MaterialTapTargetPrompt.PromptStateChangeListener()
//            {
//                @Override
//                public void onPromptStateChanged(MaterialTapTargetPrompt prompt, int state)
//                {
//                    if (state == MaterialTapTargetPrompt.STATE_FOCAL_PRESSED)
//                    {
//                        // User has pressed the prompt target
//                    }
//                }
//            })
//            .show();
        
        
        
		wv = (WebView) findViewById(R.id.mainWebsWebView);
        wvSettings = wv.getSettings();
        wvSettings.setJavaScriptEnabled(true);
        wvSettings.setSupportZoom(true);
        wvSettings.setSaveFormData(true);
        wvSettings.setSavePassword(true);
        wvSettings.setAppCacheEnabled(false);
        
        wvSettings.setJavaScriptCanOpenWindowsAutomatically(true);
        wvSettings.setBuiltInZoomControls(false);
        wvSettings.setLoadWithOverviewMode(true);
        wvSettings.setUseWideViewPort(true);
        wvSettings.setDefaultZoom(WebSettings.ZoomDensity.CLOSE);
        wv.setScrollBarStyle(View.SCROLLBARS_INSIDE_OVERLAY);
        //wv.setBackgroundColor(Color.WHITE);
        
        
        CookieManager.getInstance().setAcceptCookie(true);
        CookieManager.getInstance().setAcceptThirdPartyCookies(wv, true);
        
        wvSettings.setUserAgentString(String.valueOf(R.string.app_name));
        wvSettings.setPluginState(WebSettings.PluginState.ON);
        wvSettings.setAllowFileAccess(true);
        wvSettings.setAllowFileAccessFromFileURLs(true);
        wvSettings.setAllowContentAccess(true);
        wvSettings.setDomStorageEnabled(true);
        wvSettings.supportMultipleWindows();
        wvSettings.setLoadsImagesAutomatically(true);
        wv.loadUrl(webUrl);
        
        
        
        wv.setOnKeyListener(new OnKeyListener()
            {
                @Override
                public boolean onKey(View v, int keyCode, KeyEvent event)
                {
                    if(event.getAction() == KeyEvent.ACTION_DOWN)
                    {
                        switch(keyCode)
                        {
                            case KeyEvent.KEYCODE_BACK:
                                if(wv.canGoBack())
                                {
                                    wv.goBack();
                                    return true;
                                } else {
                                    onBackPressed();

                                }
                                break;

                        }
                    }

                    return false;
                }
            });
            
     


        wv.setWebChromeClient(new WebChromeClient()
            {
                
                
        
        
                // For api level bellow 24
                
                public boolean shouldOverrideUrlLoading(WebView view, String url) {

                    if (url.startsWith("javascript:")){
                        view.evaluateJavascript(url, null);
                        return true;
                    }
                    view.loadUrl(url);

                    return true;
                }


                // From api level 24
                @RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
                public boolean shouldOverrideUrlLoading(WebView view, WebResourceRequest request) {
                    /*Toast.makeText(mcontext, "New Method",Toast.LENGTH_SHORT).show();*/

                    // Get the tel: url
                    String url = request.getUrl().toString();
                    if (url.startsWith("javascript:")){
                        view.evaluateJavascript(url, null);
                        return true;
                    }

                    view.loadUrl(url);

                    return true;
                }

             
                
                @Override
                public void onPermissionRequest(PermissionRequest request) {
                    super.onPermissionRequest(request);
                    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
                        request.grant(request.getResources());
                    }
                }
                @Override
                public void onProgressChanged(WebView view, int progress) {
                    if(progress < 100){
                      //  pb.setVisibility(ProgressBar.VISIBLE);
                        
                    }

                   // pb.setProgress(progress);
                    if(progress == 100) {
                        
                        //pb.setVisibility(ProgressBar.GONE);
                        
                    }
                }
               
            });
            
        wv.setWebViewClient(new WebViewClient(){
           @Override
           public void onPageFinished(WebView view, String url) {
               super.onPageFinished(view, url);
               
               
               
               }
               
               
                @Override
                public void onPageStarted(WebView view, String url, Bitmap favicon) {
                    
                    
                    
                }
                
                
                
                
              
            
            
//                @Override
//                public void onReceivedError(WebView view, WebResourceRequest request, WebResourceError error) {
//                    super.onReceivedError(view, request, error);
//                    
//                    
//                    view.loadUrl("file:///android_asset/error.html");
//                    
//                    //errorPage(error.toString(), request.toString());
//                }
        });
        


        

        
        
        
        
        
        

		
        
        
        
        
       
        //tab3 = (LinearLayout) findViewById(R.id.tab3);
        
       
       
       
		//FontsOverride.setDefaultFont(this, "DEFAULT", "raleway_regular.ttf");


	}
    
            

        
    
    
    
    
    
    void checkInternet(){
       time = new Timer();
       timrr = new TimerTask(){

                @Override
                public void run() {
                    
                    runOnUiThread(new Runnable(){
                        
                        @Override
                        public void run() {
                    
                        if (!isNetworkOnline(MainActivity.this)){
                            NoConnection();
                            time.cancel();
                            time.cancel();
                            
                        
                    }
                }
                });
            }
            };
        time.schedule(timrr, 0,1000);
        
    }
    

	public static boolean isNetworkOnline(Context context) {
		ConnectivityManager manager = (ConnectivityManager) context
			.getSystemService(context.CONNECTIVITY_SERVICE);
		NetworkInfo networkInfo = manager.getActiveNetworkInfo();

		return (networkInfo != null && networkInfo.isConnectedOrConnecting());
	}




	public static SharedPreferences getSharedPreferences() {
        return sp;
    }


    
	


	public void openInCustomTab(final String url) {

		Uri websiteUri;
		if (!url.contains("https://") && !url.contains("http://")) {
			websiteUri = Uri.parse("http://" + url);
		} else {
			websiteUri = Uri.parse(url);
		}
		CustomTabsIntent.Builder customtabintent = new CustomTabsIntent.Builder();
		//customtabintent.setToolbarColor(mActivity.getResources().getColor(R.color.colorPrimary));
		customtabintent.enableUrlBarHiding();

		customtabintent.setShowTitle(false);
		if (chromeInstalled()) {
			customtabintent.build().intent.setPackage("com.android.chrome");
		}
		customtabintent.build().launchUrl(this, websiteUri);
	}
	private boolean chromeInstalled() {
		try {
			getPackageManager().getPackageInfo("com.android.chrome", 0);
			return true;
		} catch (Exception e) {
			return false;
		}
	}

	public static PackageInfo getAppInfo(Context context) {
		try {
			return context.getPackageManager().getPackageInfo(context.getPackageName(), 0);
		} catch (PackageManager.NameNotFoundException e) {
			throw new RuntimeException(e);
		}
	}

	@Override
	public void onPostCreate(Bundle savedInstanceState, PersistableBundle persistentState) {
		super.onPostCreate(savedInstanceState, persistentState);
		if (mDrawerPanel.getToogle() == null) {
			mDrawerPanel.getToogle().syncState();
		}
	}

	@Override
	public void onConfigurationChanged(Configuration newConfig) {
		super.onConfigurationChanged(newConfig);
		if (mDrawerPanel.getToogle() == null) {
			mDrawerPanel.getToogle().onConfigurationChanged(newConfig);
		}
	}
    
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        
        MenuInflater inflater = getMenuInflater();
        
        inflater.inflate(R.menu.main_menu, menu);
        
        
        return super.onCreateOptionsMenu(menu);
    }

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		if (mDrawerPanel.getToogle() == null && mDrawerPanel.getToogle().onOptionsItemSelected(item)) {
			return true;
		}
        
        switch (item.getItemId()){
            
            case R.id.refresh:
                wv.clearCache(true);
                wv.reload();
                break;
                
            case R.id.opento:
                openInCustomTab(webUrl);
                break;
                
            
                
            
                
            case R.id.tsize:
                CharSequence[] items = {"Largest","Larger","Normal", "Smallest","Smaller"};
                AlertDialog dialog = new AlertDialog.Builder(this)
                    .setTitle("Select font size")
                    .setSingleChoiceItems(items, -1, new DialogInterface.OnClickListener() {

                        @Override
                        public void onClick(DialogInterface dia, int which) {
                            switch (which){
                                case 0:
                                    wvSettings.setTextSize(WebSettings.TextSize.LARGEST);
                                    sp.edit().putInt("wfont", 0).apply();
                                    wv.reload();
                                    dia.dismiss();
                                break;
                                
                                case 1:
                                    wvSettings.setTextSize(WebSettings.TextSize.LARGER);
                                    sp.edit().putInt("wfont", 1).apply();
                                    wv.reload();
                                    dia.dismiss();
                                    break;
                                    
                                case 2:
                                    wvSettings.setTextSize(WebSettings.TextSize.NORMAL);
                                    sp.edit().putInt("wfont", 2).apply();
                                    wv.reload();
                                    dia.dismiss();
                                    break;
                                    
                                case 3:
                                    wvSettings.setTextSize(WebSettings.TextSize.SMALLEST);
                                    sp.edit().putInt("wfont", 3).apply();
                                    wv.reload();
                                    dia.dismiss();
                                    break;
                                    
                                case 4:
                                    wvSettings.setTextSize(WebSettings.TextSize.SMALLER);
                                    sp.edit().putInt("wfont", 4).apply();
                                    wv.reload();
                                    dia.dismiss();
                                    break;
                            }
                            
                            
                        }
                    })
                    .create();
                dialog.show();
                break;
                
            case R.id.exit:
                System.exit(0);
                
                break;
                
            
        }

		return super.onOptionsItemSelected(item);
	}



	

	void tinfo(String w, int e) {
		if (e == 6) {
			TastyToast.makeText(getApplicationContext(), w, 0,
								TastyToast.CONFUSING);
		}
		if (e == 5) {
			TastyToast.makeText(getApplicationContext(), w, 0,
								TastyToast.DEFAULT);
		}
		if (e == 4) {
			TastyToast.makeText(getApplicationContext(), w, 0,
								TastyToast.ERROR);
		}
		if (e == 3) {
			TastyToast.makeText(getApplicationContext(), w, 0,
								TastyToast.INFO);
		}
		if (e == 2) {
			TastyToast.makeText(getApplicationContext(), w, 0,
								TastyToast.WARNING);
		}
		if (e == 1) {
			TastyToast.makeText(getApplicationContext(), w, 0,
								TastyToast.SUCCESS);
		}

	}
    
    void checkFChanges(){
        
        int fchanges = sp.getInt("wfont", 2);
        switch (fchanges){
            case 0:
                wvSettings.setTextSize(WebSettings.TextSize.LARGEST);
            break;
                
            case 1:
                wvSettings.setTextSize(WebSettings.TextSize.LARGER);
            break;
            
            
            case 2:
                wvSettings.setTextSize(WebSettings.TextSize.NORMAL);
            break;
            
            
            case 3:
                wvSettings.setTextSize(WebSettings.TextSize.SMALLEST);
            break;
            
            
            case 4:
                wvSettings.setTextSize(WebSettings.TextSize.SMALLER);
            break;
        }
    }

	@Override
	protected void onResume() {
		super.onResume();
        
        
        checkFChanges();
        //checkAcc();
        

	}

	@Override
	public void onBackPressed() {
		super.onBackPressed();
	}

    
    


	public void updateApp() {
        new Updater(MainActivity.this, "https://pastebin.com/raw/ZTcLKEpj", new Updater.Listener() {


                @Override
                public void onLoading() {
					tinfo("Please wait..", 5);
				}
                @Override
                public void onCompleted(final String config) {
                    try {
                        final JSONObject obj = new JSONObject(config);
						String versionName = getApplicationContext().getPackageManager()
							.getPackageInfo(getApplicationContext().getPackageName(), 0).versionName;
                            
						if (versionName.equals(obj.getString("versionCode"))) {

							tinfo("App is up-to-date", 1);
                        } else {

							//notif2();
                            new AlertDialog.Builder(MainActivity.this)
                                .setTitle("New Update Available!")
								.setCancelable(true) 


                                .setMessage(obj.getString("Message"))
                                .setPositiveButton("UPDATE", new DialogInterface.OnClickListener() {
                                    @Override
                                    public void onClick(DialogInterface p1, int p2) {
                                        try {
											startActivity(new Intent(Intent.ACTION_VIEW,
																	 Uri.parse(obj.getString("url"))));
                                        } catch (JSONException e) {}
									}
                                })
								.setNegativeButton("CANCEL", null)
                                .create()
                                .show();
                        }
                    } catch (Exception e) {
						tinfo("Error occured", 2);
                        // Toast.makeText(MainActivity.this, e.getMessage() , 0).show();
                    }

                }


                @Override
                public void onCancelled() {

                }

                @Override
                public void onException(String ex) {

                }
            }).execute();


    }
    
    void NoConnection() {
       SweetAlertDialog aa = new SweetAlertDialog(MainActivity.this, SweetAlertDialog.WARNING_TYPE);
            aa.setTitleText("No Connection");
            aa.setContentText("Please connect to the internet!");
            aa.setConfirmText("Refresh");
           
            aa.setCancelable(false);
            aa.setCanceledOnTouchOutside(false);
            aa.setConfirmClickListener(new SweetAlertDialog.OnSweetClickListener(){

                @Override
                public void onClick(SweetAlertDialog p1) {
                    wv.reload();
                    p1.dismiss();
                }
                
            });
            aa.setCancelText("Exit");
        aa.setCancelClickListener(new SweetAlertDialog.OnSweetClickListener(){

                @Override
                public void onClick(SweetAlertDialog p1) {
                    System.exit(1);
                }
                
                
            });
            
            aa.show();
    }
    
    void errorPage(String des, String tit) {
        SweetAlertDialog aa = new SweetAlertDialog(MainActivity.this, SweetAlertDialog.WARNING_TYPE);
        aa.setTitleText(tit);
        aa.setContentText(des);
        aa.setConfirmText("Refresh");

        aa.setCancelable(false);
        aa.setCanceledOnTouchOutside(false);
        aa.setConfirmClickListener(new SweetAlertDialog.OnSweetClickListener(){

                @Override
                public void onClick(SweetAlertDialog p1) {
                    wv.reload();
                    p1.dismiss();
                }

            });
        aa.setCancelText("Exit");
        aa.setCancelClickListener(new SweetAlertDialog.OnSweetClickListener(){

                @Override
                public void onClick(SweetAlertDialog p1) {
                    System.exit(1);
                }


            });

        aa.show();
    }

	public void myTimer() {
        
		AdCountDown = new CountDownTimer(3000, 1000) {

			@Override
			public void onTick(long millisUntilFinished) {
				tick = millisUntilFinished;
                
                updateTost();
                button2.setText("Stop");
				nagrun = true;
			}
			@Override
			public void onFinish() {
				nagrun = false;

			}

		}.start();
       
	}

	
    

	private void updateTost() {
		int seconds = (int) (tick / 1000) % 60;
		String timeLeftFormatted;
		if (seconds > 0) {
			timeLeftFormatted = String.format(Locale.getDefault(),
											  "%02d", seconds);

			//tinfo("Wait " + timeLeftFormatted, 5);
            
		}
	}





	//###################################### DRAWERPANEL MAIN ########################################



	public class DrawerPanelMain
	implements NavigationView.OnNavigationItemSelectedListener {

		private DrawerLayout drawerLayout;
		private ActionBarDrawerToggle toggle;




		MediaPlayer player;
		private AppCompatActivity mActivity;



		public DrawerPanelMain(AppCompatActivity activity) {
			mActivity = activity;
		}




		public void setDrawer(Toolbar toolbar) {
			NavigationView drawerNavigationView = (NavigationView) mActivity.findViewById(R.id.drawerNavigationView);
			drawerLayout = (DrawerLayout) mActivity.findViewById(R.id.drawerLayoutMain);
			//changeFonts(getApplicationContext(), drawerNavigationView, "fonts/message.ttf");
			
			// set drawer
			toggle = new ActionBarDrawerToggle(mActivity,
											   drawerLayout, toolbar, R.string.open, R.string.cancel);

			drawerLayout.addDrawerListener(toggle);
			//getSupportActionBar().setDisplayHomeAsUpEnabled(true);
			toggle.syncState();



			// set app info
			PackageInfo pinfo = getAppInfo(mActivity);
			if (pinfo != null) {
				String version_nome = pinfo.versionName;
				int version_code = pinfo.versionCode;
				String header_text = String.format("v%s (%d)", version_nome, version_code);

				View view = drawerNavigationView.getHeaderView(0);

				TextView app_info_text = view.findViewById(R.id.app_info);
				app_info_text.setText(header_text);
			}
			/*    TextView version = (TextView)mActivity.findViewById (R.id.config_version_info);
			 version.setText(config.getVersion());*/

			// set navigation view
			drawerNavigationView.setNavigationItemSelectedListener(this);
		}

		public ActionBarDrawerToggle getToogle() {
			return toggle;
		}

		public DrawerLayout getDrawerLayout() {
			return drawerLayout;
		}


		@Override
		public boolean onNavigationItemSelected(@NonNull MenuItem item) {
			int id = item.getItemId();

			switch (id) {
                
                    
                case R.id.helpo:
                    tinfo("Coming Soon ~", 3);
                    break;
//				case R.id.message:
//					Intent i = new Intent(Intent.ACTION_SEND);
//					i.setType("message/rfc822");
//					i.putExtra(Intent.EXTRA_EMAIL, new String[]{"adalimlouis123@gmail.com"});
//					i.putExtra(Intent.EXTRA_SUBJECT, "Message About " +  mActivity.getString(R.string.app_name) + " ");
//					mActivity.startActivity(Intent.createChooser(i, "Send message via Email"));
//					break;

				


			    case R.id.about:

                    Intent intent = new Intent(getApplicationContext(), AboutActivity.class);
                    intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TASK);
                    startActivity(intent);
					
					break;


			}

			return true;
		}



	}

    public static int getBuildId(Context context) throws IOException {
        try {
            PackageInfo pinfo = context.getPackageManager().getPackageInfo(context.getPackageName(), 0);
            return pinfo.versionCode;
        } catch (PackageManager.NameNotFoundException e) {
            throw new IOException("Build ID not found");
        }
	}


	
    
    void welcome() {
     ca = new SweetAlertDialog(MainActivity.this, SweetAlertDialog.CUSTOM_IMAGE_TYPE);
            ca.setTitleText("Welcome User!");
            ca.setCancelable(false);
            ca.setCanceledOnTouchOutside(false);
        ca.setContentText("Welcome to G2 Speedtest app! Thank you for choosing us to measure your internet speed. Get ready to experience lightning-fast connections and accurate performance insights. We're here to help you optimize your internet experience. Start by simply tapping the \"GO\" button, and we'll take care of the rest. Happy testing!");
            ca.setCustomImage(R.drawable.logo);
            
            ca.show();
    }
    
    public void postCurl(String link, String data, String head, Vanp.Listener kk){
        new Vanp(MainActivity.this, link, head, data, kk).execute();
    }
    
    public void getCurl(String link, String head, Vans.Listener h) {
        
        
        
        new Vans(MainActivity.this, link
        , head, h).execute();


    }
    

    public static java.util.Date getDate() {
        java.util.Date date = new java.util.Date();
        return date;
    }
    
    
    
    
    
    
    
    
    
    
    
    
    
    public static void changeFonts(Context context, ViewGroup viewGroup, String fontPath) {
        AssetManager assets = context.getAssets();
        Typeface typeface = Typeface.createFromAsset(assets, fontPath);

        for (int i = 0; i < viewGroup.getChildCount(); i++) {
            View view = viewGroup.getChildAt(i);

            if (view instanceof ViewGroup) {
                changeFonts(context, (ViewGroup) view, fontPath);
            } else if (view instanceof TextView) {
                ((TextView) view).setTypeface(typeface);
            } else if (view instanceof Toolbar) {
				
			}
			
        }
    }
    public static void changeEdbg(Context context, ViewGroup viewGroup, int res) {
        //AssetManager assets = context.getAssets();
        //Typeface typeface = Typeface.createFromAsset(assets, fontPath);

        for (int i = 0; i < viewGroup.getChildCount(); i++) {
            View view = viewGroup.getChildAt(i);

            if (view instanceof ViewGroup) {
                changeEdbg(context, (ViewGroup) view, res);
            } else if (view instanceof EditText) {
                ((EditText) view).setBackground(context.getDrawable(res));
            } else if (view instanceof Toolbar) {

            }

        }
    }
    protected String getRandomAgnt() {
        String SALTCHARS = "0123456789";

        StringBuilder salt = new StringBuilder();
        Random rnd = new Random();
        while (salt.length() < 6) { // length of the random string.
            int index = (int) (rnd.nextFloat() * SALTCHARS.length());
            salt.append(SALTCHARS.charAt(index));
        }
        String saltStr = salt.toString().toLowerCase();
        String Agn = "Mozilla/5.0 (Linux; Android) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.0001."+saltStr+" Mobile Safari/537.36";
        return Agn;

    }
    
    protected String getRandomString(int length) {
        String SALTCHARS = "ABCDEFGHIJKLMNOPQRSTUVWXYZ123456789";
        
        StringBuilder salt = new StringBuilder();
        Random rnd = new Random();
        while (salt.length() < length) { // length of the random string.
            int index = (int) (rnd.nextFloat() * SALTCHARS.length());
            salt.append(SALTCHARS.charAt(index));
        }
        String saltStr = salt.toString().toLowerCase();
        return saltStr;

    }
    
    public int randNumber(int bound1, int bound2) {
        Random r = new Random();
        int low = bound1;
        int high = bound2;
        int result = r.nextInt(high-low) + low;
        return result;
    }
    
    
    
    
    
    
    public static int dp(Context context,int i) {
        return (int) TypedValue.applyDimension(1, (float) i, context.getResources().getDisplayMetrics());
    }
    
    
    
    public void showSetTimeDialog(TimePickerDialog.OnTimeSetListener h){
        Date date = getDate();
        SimpleDateFormat sd = new SimpleDateFormat("hh", Locale.getDefault());
        SimpleDateFormat sdf = new SimpleDateFormat("mm", Locale.getDefault());
        
        TimePickerDialog timePickerDialog = new TimePickerDialog(this, R.style.TimePickerTheme, h, Integer.parseInt(sd.format(date)), Integer.parseInt(sdf.format(date)), false);
        
        
        timePickerDialog.show();
    
   }

} 
