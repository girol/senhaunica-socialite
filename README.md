## Provider para utilização de senha única USP no Laravel 

Dependências em PHP:

    php-curl
    
## usage

Instalação:

    composer require uspdev/senhaunica-socialite
    
No array $listen app/Providers/EventServiceProvider.php adicione o array:

    \SocialiteProviders\Manager\SocialiteWasCalled::class => [
        'Uspdev\SenhaunicaSocialite\SenhaunicaExtendSocialite@handle',
    ],
    
Em config/services.php:

    'senhaunica' => [
        'client_id' => env('SENHAUNICA_KEY'),
        'client_secret' => env('SENHAUNICA_SECRET'),
         'redirect' => '/',
    ], 
    
    
Parâmetros no .env/.env.example:

    SENHAUNICA_KEY=fflch_sti
    SENHAUNICA_SECRET=gjgdfjk
    SENHAUNICA_CALLBACK_ID=85

Adiconar métodos em LoginController:

    use Socialite;
    public function redirectToProvider()
    {
        return Socialite::driver('senhaunica')->redirect();
    }

    public function handleProviderCallback()
    {
        $user = Socialite::driver('senhaunica')->user();
        // aqui vc pode inserir o usuário no banco de dados local, fazer o login etc.
    }

Rotas:

    Route::get('login/senhaunica', 'Auth\LoginController@redirectToProvider');
    Route::get('login/senhaunica/callback', 'Auth\LoginController@handleProviderCallback');
    
# Extras

Caso deseje ver todos parâmetros retornados no requisição, em Server.php:

    public function userDetails($data, TokenCredentials $tokenCredentials)
    {  
        var_dump($data); die();
    }
# [Hangout](https://youtu.be/jLFM2AUFJgw)
