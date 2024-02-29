=========================
EC2を作って最初にやること
=========================

ホスト名の変更
==============

EC2を作成後、ホスト名は以下のフォーマットで自動設定されています。
システムログにもこのホスト名は使われていますが、人間がもう少し読みやすいホスト名を望むならホスト名を変更しましょう。

ホスト名は以下のコマンドで変更します。以下の例ではホスト名に「al2023-001」を指定します。

.. code-block:: none

    hostnamectl set-hostname al2023-001

タイムゾーンの変更
==================

EC2作成後、デフォルトでタイムゾーンはUTCが設定されます。
これをロケールに合わせる場合は、以下のように設定します。以下は Asia/Tokyo の場合です。

.. code-block:: none

    timedatectl set-timezone Asia/Tokyo

別のタイムゾーンを設定する場合、指定できる値は以下のように調べることができます。

.. code-block:: none

    $ timedatectl list-timezones | less
    Africa/Abidjan
    Africa/Accra
    Africa/Addis_Ababa
    Africa/Algiers
    Africa/Asmara

ロケールの変更
==============

デフォルトではUTF-8でロケールが設定されています。

.. code-block:: none

    $ localectl
    System Locale: LANG=C.UTF-8
        VC Keymap: (unset)
       X11 Layout: (unset)

ロケールを日本に合わせるなら以下のように実行します。

.. code-block:: none
    
    $ localectl set-locales ja_JP.UTF-8
    $ localectl
    System Locale: LANG=ja_JP.UTF-8
        VC Keymap: (unset)
        X11 Layout: (unset)

SSMログイン用ユーザの作成とパスワードの設定
===========================================

SSMコンソールでログインする場合は、ログインプロンプトに入力するユーザ名とパスワードの指定、必要であれば管理者権限の設定が必要です。
ec2-userはパスワードが設定されていないため、SSMコンソールでログインする場合は別のユーザを作成しましょう。

.. code-block:: none

    $ sudo adduser ec2-user
    $ sudo passwd ec2-user
    Passwd:

SSMコンソールからのログインにはSSH公開鍵認証の設定は不要です。
