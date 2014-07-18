---
layout: post
comments: true
title: Android – Tela de apresentação (Splash screen)
---

Como fazer uma tela de apresentação para meu aplicativo Android?
Tive essa dúvida esses dias quando desenvolvia meu aplicativo e resolvi compartilhar como se faz.  

<!-- more -->

Essa tela de apresentação, ou splash screen, é a tela inicial que é exibida ao abrir um aplicativo. A maioria dos aplicativos apresentam splash screens, geralmente para exibir o logo do aplicativo ou da empresa que o desenvolveu.
Também pode ser uma maneira de “distrair” o usuário durante alguns segundos enquanto a aplicação realiza algum processo ou carregamento inicial.
 
Para criar uma splash screen na verdade é muito simples. Primeiramente criamos uma Activity para o Splash que implementa a classe Runnable. Implementaremos o método run para iniciar a primeira Activity após a apresentação.

{% highlight java %}
public class Splash extends Activity implements Runnable {

	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.splash);

		Handler handler = new Handler();
		handler.postDelayed(this, 3000);
	}

	public void run(){
		startActivity(new Intent(this, OutraClasse.class));
		finish();
	}
}
{% endhighlight %}

O Handler tem duas funções principais para qual ele pode ser utilizado. Agendar mensagens e ações a serem executadas em algum momento no futuro ou separar uma ação para ser executada em uma outra thread. Usaremos o método postDelayed que executará o runnable após o tempo especificado.  
 
Precisamos alterar o AndroidManifest.xml para especificar a Activity que será invocada ao iniciar a aplicação.

{% highlight xml %}
<application android:icon="@drawable/projeto" android:label="@string/app_name" android:debuggable="true">
    
  <activity android:name="Splash" android:label="@string/app_name">
    <intent-filter>
       <action android:name="android.intent.action.MAIN" />
       <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
  </activity>
        
  <activity android:name="OutraClasse" android:label="@string/app_name">
    <intent-filter>
       <action android:name="android.intent.action.MAIN" />
    </intent-filter>
  </activity>
</application>
{% endhighlight %}

E criar uma view onde ficará a imagem a ser exibida na apresentação do aplicativo.

{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent">

	<ImageView
 		android:layout_width="wrap_content"
 		android:layout_height="fill_parent"
 		android:layout_gravity="center"
 		android:src="@drawable/imagem"/>

</LinearLayout>
{% endhighlight %}


É isso ai. Simples não?

:)
