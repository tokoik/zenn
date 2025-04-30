---
title: "プログラムの作成"
free: true
---

## GLFW の導入

OpenGL はプラットホームに組み込まれていますが、1.5.1節で述べた通り、この呼び出し方法はプラットホームごとに異なります。そこで、この講義では各プラットホームでソースコードを共通にするために、ツールキットの GLFW (<http://www.glfw.org>) を利用します。GLFW は別途導入する必要があります。

### Windows への導入

GLFW のプロジェクトのダウンロードページ (<http://www.glfw.org/download.html>) の “32-bit Windows binaries” のボタンをクリックしてください。すると 32bit 版のバイナリファイルをまとめた ZIP ファイル glfw-3.X.Y.bin.WIN32.zip (X, Y は数字) がダウンロードされますから、これを右クリックで選択して「すべて展開」を選び、書き込み可能な適当なディレクトリ (マイドキュメント、デスクトップ、C:\\ など) に展開してください。

パソコンの管理者権限を持っている場合は、この中のフォルダやファイルを以下の「システムのディレクトリ」 (Visual Studio 2013 の場合) に移動あるいはコピーしてください。これにより、プロジェクトの作成時に「VC++ ディレクトリ」を設定する手間を省くことができます。

#### 32bit 版 Windows の場合

> include フォルダにある GLFW フォルダ
>
> C:\Program Files\Windows Kits\8.1\Include\um
>
> lib-msvc120 フォルダにある glfw3.lib ファイル
>
> C:\Program Files\Windows Kits\8.1\Lib\winv6.3\um\x86

#### 64bit 版 Windows の場合

> include フォルダにある GLFW フォルダ
>
> C:\Program Files (x86)\Windows Kits\8.1\Include\um
>
> lib-msvc120 フォルダにある glfw3.lib ファイル
>
> C:\Program Files (x86)\Windows Kits\8.1\Lib\winv6.3\um\x86

パソコンの管理者権限を持っていない場合は、Visual Studio のプロジェクト作成時に、「VC++ ディレクトリ」に ZIP ファイルを展開したディレクトリ (フォルダ) を指定します。この方法は後述します。

なお、ソースファイルからコンパイルする場合は CMake (<http://www.cmake.org>) を利用します。CMake (cmake-gui) を起動して “Where is the source code” にソースファイルの ZIP ファイルを展開したディレクトリを指定し、“Where to build the binaries” には書き込み可能なディレクトリを指定します。その後、“Configure” をクリックして使用する Visual Studio のバージョンを指定した後 “Generate” をクリックすれば、Visual Studio のプロジェクトファイルが作成されます。

### Mac OS X

Mac OS X では、Xcode と Command Line Tools がインストールされている必要があります。Xcode は AppStore から無料で入手できます。Command Line Tools は、Xcode のバージョン 5 には同梱されていますが、“Xcode” メニューから “Open Developer Tool” の “More Developer Tools” を選ぶとダウンロードページが表示されます (無料の開発者ユーザ登録が必要です)。

本稿の執筆時点では、MacPorts (<http://www.macports.org>) に GLFW のバージョン 3 のパッケージが用意されていましたが、HomeBrew (<http://brew.sh>) や Fink (<http://www.finkproject.org>) にはありませんでした。ソースファイルからは以下の手順でインストールできます。

#### インストール

GLFW のプロジェクトのダウンロードページ (<http://www.glfw.org/download.html>) からソースファイルの ZIP ファイル glfw-3.X.Y.zip (X, Y は数字) をダウンロードしてデスクトップに置き、それをダブルクリックして展開してください。glfw-3.X.Y というディレクトリが作成されます。

次にターミナルを開き、以下のコマンドを順に実行してください (管理者権限が必要です)。‘%’ はシェルのプロンプトを表します。なお、ファイルは /usr/local 以下にインストールされます。

> % cd ~/Desktop/glfw-3.X.Y  
> % mkdir build  
> % cd build  
> % cmake ..  
> % make  
> % sudo make install

#### アンインストール

インストールした GLFW のファイルを削除する必要が生じた場合は、前述の手順で GLFW をインストールしたときに build ディレクトリの中に作成される Makefile を使ってアンインストールできます (管理者権限が必要です)。

> % cd ~/Desktop/glfw-3.X.Y/build  
> % sudo make uninstall

### Linux

Linux (X11) は NVIDIA GeForce 8 シリーズ以降あるいは ATI RADEON HD シリーズ以降のビデオカードで、プロプライエタリドライバがインストールされていることを想定しています。Intel の CPU 内蔵グラフィックスの場合、ドライバは <https://01.org> から入手できます。

本稿の執筆時点では、Fedora (<http://fedoraproject.org>) に GLFW のバージョン 3 のパッケージが用意されていましたが、Ubuntu (<http://www.ubuntu.com>) や OpenSUSE (<http://www.opensuse.org>) にはありませんでした。ソースファイルからは以下の手順でインストールできます。

#### インストール

GLFW のプロジェクトのダウンロードページ (<http://www.glfw.org/download.html>) からソースファイルの ZIP ファイル glfw-3.X.Y.zip (X, Y は数字) ダウンロードしてください。

次にターミナルを開き、以下のコマンドを順に実行してください (管理者権限が必要です)。‘%’ はシェルのプロンプトを表します。なお、ファイルは /usr/local 以下にインストールされます。

> % unzip glfw-3.X.Y.zip  
> % cd glfw-3.X.Y  
> % mkdir build  
> % cd build  
> % cmake ..  
> % make  
> % sudo make install

#### アンインストール

インストールした GLFW のファイルを削除する必要が生じた場合は、前述の手順で GLFW をインストールしたときに build ディレクトリの中に作成される Makefile を使ってアンインストールできます (管理者権限が必要です)。

> % cd glfw-3.X.Y/build  
> % sudo make uninstall

## ソフトウェア開発環境

プログラムの作成はテキストエディタとコンパイラ・リンカなどの言語処理系さえあれば可能ですが、現在はテキストエディタやコンパイラ・リンカ、デバッガなどをひとまとめにした、統合開発環境 (Integrated Development Environment, IDE) が一般的に用いられます。ここでは各プラットホームにおいてよく使われるソフトウェア開発環境について説明します。

### Windows

#### プロジェクトの新規作成

Windows では Visual Studio 2013 を例にして説明します。Visual Studio 2013 を起動し、新しいプロジェクトを作成してください。新しいプロジェクトを作成するには、「ファイル」のメニューの「新規作成」から「プロジェクト」を選ぶか、図 28の矢印のところをクリックします。

図 28 プロジェクトの作成

インストール済みのテンプレートから「Visual C++」の「Win32 コンソールアプリケーション」を選び、作成するプログラムの「名前」を設定してから「OK」をクリックしてください (図 29)。

図 29 「Win32 コンソールアプリケーション」の選択

作成するプロジェクトの設定を変更するので、図 30 では「次へ」をクリックします。

図 30 「次へ」をクリック

「追加のオプション」のウィンドウ (図 31) で「空のプロジェクト」を選択します。これを選択しなければ main() 関数を含むソースファイルが作成されますが、それを使用しても構いません。最後に「完了」をクリックしてください。

図 31 「空のプロジェクト」の選択

#### プロジェクトのプロパティ

このプロジェクトで、GLFW を使用する設定を行います。「プロジェクト」のメニューの「プロパティ」を選択してください (図 32)。

図 32 プロジェクトの「プロパティ」の設定

図 33 プロジェクトの「構成」の選択

図 33 のプロジェクトの構成には、デバッグのときに用いる「デバッグ」と、デバッグが完了して最終的なプログラムを作成するときに用いる「リリース」が用意されています。「リリース」構成でプログラムをビルド (コンパイルやリンク等の一連の処理を経て目的のプログラムを作成する作業) すると最適化により効率の良いプログラムが生成されますが、不要なコードが削除されたりするためにソースプログラムとコンパイルした結果が一致しなくなり、デバッグが難しくなります。ここでは両方の構成に同じ設定を適用するために、「全ての構成」を選びます。

#### 「VC++ ディレクトリ」の設定 (ファイルを「システムのディレクトリ」に置いた時は不要)

GLFWのヘッダファイルやライブラリファイルの場所を設定します。プロパティページのウィンドウ (図 34) の左側のペイン (ウィンドウの領域) で「VC++ ディレクトリ」を選び、「インクルードディレクトリ」の欄の右端の▼をクリックして、\<編集…\> を選んでください。

図 34 「インクルードディレクトリ」の項目の編集

「インクルードディレクトリ」の設定ウィンドウ (図 35) の右上のフォルダのアイコンをクリックすると、欄がひとつ作成されます。その欄の右側の「…」をクリックしてください。

図 35 「インクルードディレクトリ」の設定ウィンドウ

ディレクトリの選択のダイアログウィンドウ (図 36) が現れるので、GLFW のバイナリファイルの ZIP ファイルを展開したディレクトリの中の include ディレクトリを選択して、「フォルダーの選択」をクリックしてください。

図 36 GLFW のパッケージの include ディレクトリの選択

以上の設定が完了したら、「OK」をクリックしてください (図 37)。

図 37 「インクルードディレクトリ」の設定完了

「ライブラリディレクトリ」の欄の右端の▼をクリックして、\<編集…\> を選びます (図 38)。

図 38 「ライブラリディレクトリ」の項目の編集

「ライブラリディレクトリ」の設定ウィンドウ (図 39) の右上のフォルダのアイコンをクリックして、欄をひとつ作成します。その後、その欄の右側の「…」をクリックしてください。

図 39 「ライブラリディレクトリ」の設定ウィンドウ

GLFW のバイナリファイルの ZIP ファイルを展開したディレクトリの中の lib-msvc120 ディレクトリを選択して、「フォルダーの選択」をクリックしてください (図 40)。

図 40 GLFW パッケージの lib-msvc120 ディレクトリの選択

以上の設定が完了したら、「OK」をクリックしてください (図 41)。

図 41 「ライブラリディレクトリ」の設定完了

#### リンクするライブラリファイルの指定

プログラムのリンク時にリンクする GLFW と OpenGL のライブラリファイルを指定します。プロパティページのウィンドウ (図 42) の左側のペインで「リンカー」「入力」の順に選択し、「追加の依存ファイル」の欄の右端の▼をクリックして、\<編集…\> を選んでください。

図 42 追加の依存ファイル

リンクするライブラリファイルとして、glfw3.lib, opengl32.lib の二つを「追加の依存ファイル」に追加します (図 43)。その後、「OK」をクリックしてください。

図 43 glfw3.lib と opengl32.lib の追加

図 44 追加後の「追加の依存ファイル」

追加後の「追加の依存ファイル」は図 44のようになります。ここに直接 “glfw3.lib; opengl32.lib;” を入力することもできます。最後に「OK」をクリックしてください。

##### 補足：ソースプログラムへの設定の埋め込み

「リンクするライブラリファイルの指定」はソースプログラム (複数ある場合は、どれかひとつだけで構いません) に次の 2 行を置くことにより、省くことができます。

> \#pragma comment(lib, "glfw3.lib")
>
> \#pragma comment(lib, "opengl32.lib")

したがって、GLFW 関連のファイルを「システムのディレクトリ」に置き、ソースプログラムの冒頭でこれらの設定を行えば、プロジェクトを新規作成するたびに「プロジェクトのプロパティ」を設定する手間を省くことができます。

また、「Win32 コンソールアプリケーション」のプロジェクトで作成したプログラムは、実行すると OpenGL のウィンドウのほかに「コンソールウィンドウ」が開きます。コンソールウィンドウはデバッグ時にメッセージ等を表示するのに有用ですが、これを開きたくない場合は次の内容をソースプログラムに追加してください (続けて 1 行で入力してください)。

> \#pragma comment(linker, "/subsystem:\\windows\\ /entry:\\mainCRTStartup\\")

##### 補足：ライブラリのリンクについて

ライブラリのリンク方法には、スタティックリンクとダイナミックリンクという二つの方法があります。スタティックリンクは、ライブラリファイルに登録されている関数をプログラムのリンク時にプログラム自体に組み込む方法です。一方ダイナミックリンクは、ライブラリファイルを別に用意しておき、プログラムの実行時にそのライブラリファイルに登録されている関数を呼び出す方法です。この別に用意したライブラリファイルのことを、ダイナミックリンクライブラリ (Dynamic Link Library, DLL) と呼びます。

ライブラリファイルに登録されている関数は複数のプログラムから利用されるため、スタティックリンクを行うと同じ関数のコピーが異なるプログラム内に存在することになり、メモリやディスクなどが無駄に使われます。これに対してダイナミックリンクでは、関数の実体はひとつになるため、スタティックリンクのような無駄がありません。また、ライブラリが更新されたときは DLL を入れ替えるだけで済み、スタティックリンクのようにリンクし直す必要がありません。

このようにメリットの多いダイナミックリンクですが、本書ではスタティックリンク用のライブラリである glfw3.lib をリンクしています。この理由は、ダイナミックリンクでは DLL を「コマンドの検索パス」に含まれるディレクトリや「作業ディレクトリ」に置くことを嫌ったためです。また、DLL のバージョンの不一致によるトラブルを避けることにも配慮しています。

しかし、Visual C++ においてこれらのスタティックリンク用のライブラリをリンクすると、Visual C++ によって暗黙的にリンクされる他のライブラリと競合しているという警告が表示されることがあります。この警告はダイナミックリンクを行えば抑制することができます。

GLFW をダイナミックリンクするには glfw3.lib の代わりに glfw3dll.lib をリンクします。これはプログラムから DLL (glfw3.dll) を呼び出すためのライブラリです。そして、この glfw3.dll を「コマンドの検索パス」に含まれるディレクトリか、作成したプログラムを実行する際の「作業ディレクトリ」に置いてください。前者の場合は glfw3.dll を「システムのディレクトリ」である C:\Windows\System32 (32bit 版 Windows) あるいは C:\Windows\SysWOW64 (64bit 版 Windows) に置くか、「システムの詳細設定[^3]」で「システム環境変数」の Path に glfw3.dll を置いたディレクトリを追加してください。

#### ソースファイルの追加

プログラムのソースファイルを作成します。「プロジェクト」のメニューから「新しい項目の追加」を選んでください (図 45)。

図 45 新しい項目の追加

「新しい項目の追加」のウィンドウ (図 46) の左側のペインで「Visual C++」を選び、中央のペインで「C++ ファイル (.cpp)」を選んでください。また、その下の「名前」の欄にソースファイルのファイル名を入力してください。その後、「追加」をクリックしてください。

図 46 C++ のソースファイルの追加（新規作成）

テキストエディタのウィンドウ (図 47) が開きます。ここにソースプログラムを入力します。

図 47 ソースプログラムの編集

### Mac OS X

#### プロジェクトの新規作成

Mac OS X では Xcode のバージョン 5 の例について説明します。Xcode を起動し、スプラッシュウィンドウ (図 48) の “Create a new Xcode project” をクリックするか、“File” メニューの “New” から “Project” を選んでください。

図 48 スプラッシュウィンドウ

プロジェクトのテンプレートとして “OS X” の “Application” から “Command Line Tool” を選び、“Next” をクリックしてください (図 49)。

図 49 プロジェクトのテンプレートの選択

プロジェクトのオプションは、“Product Name” だけ設定してください。“Organization Name” や “Company Identifier” は既定値が設定されています。“Type” にはもちろん C++ を選んでください。その後 “Next” をクリックしてください (図 50)。

図 50 プロジェクトのオプションの設定

プロジェクトのディレクトリを作成する場所を指定します。適当なところを選んで、“Create” をクリックしてください (図 51)。

図 51 プロジェクトのディレクトリの保存先

#### プロジェクトの設定

まず、ヘッダファイルとライブラリの検索パスを設定します。図 52 のウィンドウの左側にあるプロジェクト名をクリックし、その右のポップアップメニューから “Targets” を選んでください。次に中央部の “Build Settings” を選択します。ここには設定項目が大量にあるので、検索窓に “search” などを入力して “Header Search Paths” という項目を探し、その右側をダブルクリックします。すると入力ウィンドウがポップアップしますから、左下の “+” をクリックして欄を追加し、そこに GLFW のヘッダファイルをインストールした場所 (/usr/local/include) を設定してください。

図 52 ヘッダファイルの検索パスの設定

ポップアップしたウィンドウは ESC キーをタイプするか、そのウィンドウ以外のところをクリックすれば消えます。次に “Library Search Paths” の右側 (図 53) をダブルクリックし、同様に GLFW のライブラリファイルをインストールした場所 (/usr/local/lib) を設定します。

図 53 ライブラリファイルの検索パスの設定

リンクするライブラリとフレームワークを設定します。検索窓に “linker” などを入力して “Other Linker Flags” という項目を探し、その右側をダブルクリックします (図 54)。入力ウィンドウがポップアップしたら、左下の “+” をクリックして欄を追加し、そこに以下の内容を入力してください。これは 1 行で入力しても、ひとつずつ欄を作っても構いません。

> -lglfw3 -framework Cocoa -framework IOKit -framework OpenGL -framework CoreVideo

図 54 リンクするライブラリとフレームワークの指定

このテンプレートでは “main.cpp” というファイル名のソースファイルが自動的に作成されます (図 55)。これに main() 関数が定義されています。また “プロジェクト名.1” は Unix や Linux で使われる man 形式のマニュアルのソースファイルです。本書ではこれは使わないので、右クリックして選択して “Delete” を選んで削除しても構いません。

図 55 ソースプログラムの編集

#### Makefile を作る

Xcode を使用せず、シェルでコマンドを使ってプログラムを作成する場合は、Makefile を用意しておくと手間が省けます。まず、mkdir コマンドなどを使って、ソースファイルを置く空のディレクトリをひとつ作成してください。‘%’ はシェルのプロンプトを表します。

> % mkdir sample

次に、テキストエディタを使って以下の内容のファイルを Makefile というファイル名で作成し、このディレクトリに保存してください。また、このファイルの行頭の空白 (網かけの部分) には、スペースではなくタブを使ってください。

> CXXFLAGS = -I/usr/local/include –Wall  
> LDLIBS = -L/usr/local/lib -lglfw3 -framework Cocoa -framework IOKit \\  
> -framework OpenGL -framework CoreVideo  
> OBJECTS = \$(patsubst %.cpp,%.o,\$(wildcard \*.cpp))  
> TARGET = sample  
>   
> .PHONY: clean  
>   
> \$(TARGET): \$(OBJECTS)
>
> \$(LINK.cc) \$^ \$(LOADLIBES) \$(LDLIBS) -o \$@
>
> clean:  
> -\$(RM) \$(TARGET) \$(OBJECTS) \*~ .\*~ core

このファイルを作成しておけば、このディレクトリで make コマンドを実行することにより、ソースプログラムがコンパイル・リンクされて、実行プログラムが作成されます。

### Linux

#### Geany を使う

Linux にもさまざまな統合開発環境があり、また、本書の執筆時点ではどれが主流というわけでもなさそうです。テキストエディタとコマンドラインコンパイラだけで開発することも可能なのですが、ここではシンプルで軽量な開発環境の Geany (<http://www.geany.org>) の例を紹介します。

ターミナルを開き、次のコマンドで Geany を起動して、テキストファイルを新規作成します。この例では main.cpp というファイル名のソースファイルを作成します。‘%’ はシェルのプロンプトを表します。

> % geany main.cpp

あるいは、Geany の「ファイル」メニューから新規作成することもできます。C++ のソースファイルであれば、「テンプレートから新規作成」の main.cxx を選びます (図 56)。拡張子が “.cxx” になってしまいますが、Linux ではこれも C++ のソースファイルの拡張子として認識されます。

図 56 ソースファイルの新規作成

図 57 ビルドコマンドの設定ウィンドウの呼び出し

次に、コンパイルオプションの設定を行います。Geany の「ビルド」メニューから「ビルドコマンドを設定」を選んでください (図 57)。「ビルドコマンドを設定」のウィンドウの「ビルド」ラベルのコマンドの欄 (図 58) に、既に入力されているものの後にスペースをあけて次の内容を追加してください。-lm は GLFW あるいは OpenGL では利用されませんが、本書のプログラムでは数学ライブラリを使うので、ここで追加しておきます。

> -lGL -lglfw3 -lXi -lXrandr -lXxf86vm -lX11 -lrt -lpthread -lm

設定が終わったら「OK」をクリックしてください。

図 58 ビルドコマンドを設定

#### Makefile を作る

Geany などの統合開発環境を使用せず、シェルでコマンドを使ってプログラムを作成する場合は、Makefile を用意しておくと手間が省けます。まず、mkdir コマンドなどを使って、ソースファイルを置く空のディレクトリを作成してください。‘%’ はシェルのプロンプトを表します。

> % mkdir sample

次に、テキストエディタを使って以下の内容のファイルを Makefile というファイル名で作成し、このディレクトリに保存してください。また、このファイルの行頭の空白 (網かけの部分) には、スペースではなくタブを使ってください。

> CXXFLAGS = -Wall  
> LDLIBS = -lGL -lglfw3 -lXi -lXrandr -lXxf86vm -lX11 -lrt -lpthread –lm  
> OBJECTS = \$(patsubst %.cpp,%.o,\$(wildcard \*.cpp))  
> TARGET = sample  
>   
> .PHONY: clean  
>   
> \$(TARGET): \$(OBJECTS)  
> \$(LINK.cc) \$^ \$(LOADLIBES) \$(LDLIBS) -o \$@  
>   
> clean:  
> -\$(RM) \$(TARGET) \$(OBJECTS) \*~ .\*~ core

このファイルを作成しておけば、このディレクトリで make コマンドを実行することにより、ソースプログラムがコンパイル・リンクされて、実行プログラムが作成されます。

## ソースプログラムの作成

### 処理手順

この講義では、講義内容をもとに実際にプログラムを作成し、講義内容の理解と定着を図ります。理論的な部分は OpenGL を用いて実装しますが、それを実際に動作させるためにはアプリケーションプログラムとしての枠組みが必要になります。そのためのツールキットとして、この講義では GLFW を採用します。GLFW を使ったプログラムの処理手順は次のようになります。

1)  GLFW を初期化する (glfwInit())

2)  ウィンドウを作成する (glfwCreateWindow())

3)  ウィンドウが開いている間くり返し描画する (glfwWindowShouldClose())

4)  ダブルバッファリングのバッファの入れ替えを行う (glfwSwapBuffers())

5)  ウィンドウが閉じたら終了処理を行う (glfwTerminate())

そこで、最初に「最小の」C++ のプログラムを考えてみます。以下の網かけの部分を (使用するソフトウェア開発環境の) テキストエディタに打ち込んでください。

> int main()  
> {  
> }

このプログラムは、プログラムのエントリポイント (プログラムの実行を開始する場所) である main() 関数しかなく、その中身も空なので、実行しても何も起こらずに終了します。

### GLFW の初期化

main() 関数に GLFW の初期化処理を追加します。ソースプログラムの冒頭でGLFW のヘッダファイル GLFW/glfw3.h を \#include し、main() 関数の最初の部分、すなわちプログラムの実行開始直後に glfwInit() 関数を実行します。これにより、このプログラムで OpenGL を使用するための準備が行われます。glfwInit() 関数の戻り値が GL_FALSE のときは GLFW の初期化に失敗していますから、エラーメッセージを出してプログラムを終了するようにします。

> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
> }

int glfwInit(void)

> GLFW を初期化します。他の全ての GLFW の関数を実行する前に実行する必要があります。初期化に成功すれば GL_TRUE、失敗すれば GL_FALSE を返します。

### ウィンドウを作成する

GLFW の初期化が成功したら、glfwCreateWindow() 関数を使って OpenGL による描画を行うウィンドウを作成します。glfwCreateWindow() 関数の戻り値は、レンダリングコンテキストと呼ばれるウィンドウ固有の情報を含むオブジェクトのポインタです。ここで何らかの理由によりウィンドウが作成できなかった場合には、これが NULL になりますので、そのときはエラーメッセージを表示してプログラムを終了するようにしておきます。なお、この時点では既に glfwInit() による GLFW の初期化が完了していますので、プログラムを終了する直前、すなわち return 文の前で、glfwTerminate() 関数を実行して GLFW の終了処理を行います。

> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> glfwTerminate();  
> return 1;  
> }  
> }

GLFWwindow \*glfwCreateWindow(int width, int height, const char \*title, GLFWmonitor \*monitor, GLFWwindow \*share)

> GLFW のウィンドウを作成します。戻り値は作成したウィンドウのハンドルです。ウィンドウが開けなければ NULL を返します。
>
> width

作成するウィンドウの横幅の画素数で、0 より大きくなければなりません。

> height

作成するウィンドウの高さの画素数で、0 より大きくなければなりません。

> title

作成するウィンドウのタイトルバーに表示する文字列です。文字コードは UTF-8 です。

> monitor

ウィンドウをモニタ (ディスプレイ) の全面に表示するとき (フルスクリーンモード)、表示するモニタを指定します。フルスクリーンモードでなければ NULL を指定します。

> share

引数 share に他のウィンドウのハンドルを指定すれば、そのウィンドウとテクスチャなどのリソースを共有します。NULL を指定すれば、リソースの共有は行いません。

void glfwTerminate(void)

> GLFW の終了処理を行います。glfwInit() 関数で GLFW の初期化に成功した場合は、プログラムを終了する前に、この関数を実行する必要があります。この関数は GLFW で作成した全てのウィンドウを閉じ、確保した全てのリソースを解放して、プログラムの状態を glfwInit() 関数で初期化する前に戻します。この後に GLFW の機能を使用するには、再度 glfwInit() 関数を実行しなければなりません。

### 作成したウィンドウを処理対象にする

ウィンドウを作成することに成功したら、glfwMakeContextCurrent() 関数の引数にそのハンドルを指定して、そのウィンドウのレンダリングコンテキストを処理の対象にします。開いたウィンドウに対する設定や図形の描画などは、この後に行います。

> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> glfwTerminate();  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
> }

void glfwMakeContextCurrent(GLFWwindow \*const window)

> 引数 window に指定したハンドルのウィンドウのレンダリングコンテキストをカレント (処理対象) にします。レンダリングコンテキストは描画に用いられる情報で、ウィンドウごとに保持されます。図形の描画はこれをカレントに設定したウィンドウに対して行われます。
>
> window

OpenGL の処理対象とするウィンドウのハンドルを指定します。

### OpenGL の初期設定

glfwMakeContextCurrent() 関数で OpenGL による描画を行うウィンドウを指定すれば、ようやく OpenGL の機能が使用できるようになります。ここでは glClearColor() 関数により画面を消去する色を指定します。表示領域を消去する色 (背景色) は、ここでは白にします。なお、関数名が gl〜 で始まるものは OpenGL の API です (GLFW の関数名は glfw〜 で始まります)。

> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> glfwTerminate();  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
> }

void glClearColor(GLclampf R, GLclampf G, GLclampf B, GLclampf A)

> glClear(GL_COLOR_BUFFER_BIT) でウィンドウを塗り潰す色を指定します。
>
> R，G，B

それぞれ赤、緑、青色の成分の強さを示す GLclampf 型 (float 型と等価) の値で、0～1 の値を持ちます (図 59)。1 が最も明るく、この三つにそれぞれ 0, 0, 0 を指定すれば黒色、1, 1, 1 を指定すれば白色になります。

> A

アルファ値と呼ばれ、OpenGL では不透明度として扱われます (0 で透明、1 で不透明)。ここではとりあえず 0 にしておきます。

図 59 R, G, B の値と色

### メインループ

ウィンドウを開いても、このままではすぐに main() 関数の最後に到達して、プログラムが終了してしまいます。そこで、ウィンドウが閉じられなければプログラムが終了しないように、while によって処理を繰り返します。ウィンドウが閉じられたかどうかは、glfwWindowShouldClose() const 関数で調べることができます。

このループの中では、最初に glClear() 関数を使って画面の表示領域を消去します。その後、そこに OpenGL により図形の描画を行います。描画が終わったら glfwSwapBuffers() 関数を実行して、図形を描画したカラーバッファと現在図形を表示しているカラーバッファを入れ替えます。この処理はダブルバッファリングといいます。

最後に、このプログラムが次に何をすべきか判断するために、この時点で発生しているイベントを調査します。glfwWindowShouldClose() const によるウィンドウを閉じるべきかどうかの判断も、このイベントの調査にもとづいて行われます。イベントの調査には、マウスなどで操作する対話的なアプリケーションの場合は、イベントが発生するまで待つ glfwWaitEvents() 関数を用います。これに対して、時間とともに画面の表示を更新するアニメーションなどの場合は、イベントの発生を待たない glfwPollEvents() 関数を用います (表 2)。

> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> glfwTerminate();  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
>   
> // ウィンドウが開いている間繰り返す  
> while (glfwWindowShouldClose(window) == GL_FALSE)  
> {  
> // ウィンドウを消去する  
> glClear(GL_COLOR_BUFFER_BIT);  
>   
> //  
> // ここで描画処理を行う  
> //  
>   
> // カラーバッファを入れ替える  
> glfwSwapBuffers(window);  
>   
> // イベントを取り出す  
> glfwWaitEvents();  
> }  
> }

int glfwWindowShouldClose(GLFWwindow \*const window)

> window に指定したウィンドウを閉じる必要があるとき、戻り値は非 0 になります。

void glClear(GLbitfield mask)

> ウィンドウを塗り潰します。mask には塗り潰すバッファを指定します。フレームバッファは色を格納するカラーバッファのほか、隠面消去処理に使うデプスバッファ、図形の型抜きを行うステンシルバッファなどの複数のバッファで構成されており (図 27)、これらがひとつのウィンドウに重なっています。mask に GL_COLOR_BUFFER_BIT を指定したときは、カラーバッファだけを glClearColor() 関数で指定した色で塗り潰します。

void glfwSwapBuffers(GLFWwindow \*const window)

> window に指定したウィンドウのカラーバッファを入れ替えます。図形を描画した後にこの関数を実行しなければ、描画したものは画面に表示されません。

void glfwWaitEvents(void)

> マウスの操作などのイベントの発生を待ちます。イベントが発生したら、それを記録してプログラムの実行を再開します。アニメーションのように画面表示を常に更新し続けるような必要がなければ、コンピュータの負荷を低減するために、この関数を用います。ただし、この関数はメインのループ以外で実行すべきではありません。

void glfwPollEvents(void)

> マウスの操作などのイベントを取り出し、それを記録します。この関数はプログラムを停止させないので、アニメーションのように連続して画面表示を更新する場合に使用します。

表 2 イベントの取り出し

#### 補足：バッファについて

バッファは一般に緩衝装置と訳されます。これは何か二つのものが接続されており、一方からもう一方に何らかの影響を与えるような状況にあるとき、この二つの間に入って影響の仲立ちをするもののことをいいます。

OpenGL におけるバッファは、データを次の処理に引き渡すために用いる、メモリのことを指します。OpenGL ではいろいろな種類のバッファを使用しますが、ここで用いているバッファは、描画した図形を画面に表示するために用いるフレームバッファのカラーバッファです。

図形はフレームバッファのカラーバッファに描画されます。画面上への表示は、このカラーバッファの内容を読み出しながら映像信号を発生することにより行います。ここでフレームバッファへの描画と読み出しを同時に行うと、表示にちらつきが発生してしまいします。そこでカラーバッファを二つ用意しておいて、一方を表示している間にもう一方に描画するようにします。そして、描画が完了した時点でこの二つのカラーバッファを入れ替えます (図 60)。この処理をダブルバッファリングといいます。

図 60 ダブルバッファリング

#### 補足：イベントについて

画面上に複数のウィンドウが存在する場合、図形を表示しているウィンドウの上に重なっている他のウィンドウが閉じられた場合には、下のウィンドウの表示内容を描き直す必要があります。また対話的なアプリケーションでは、マウスなどの操作に対応した処理を随時実行する必要があります。このように、ある処理の実行のきっかけとなる出来事を、イベントと呼びます。

発生したイベントに対応する処理の実行方法には、画面表示のたびに glfwWaitEvents() 関数や glfwPollEvents() 関数を用いてイベントを取り出す方法 (ポーリング方式) と、特定のイベントが発生したときに実行する関数をあらかじめ登録しておく方法 (コールバック方式) があります。

### 終了処理

glfwInit() 関数による初期化に成功していれば、プログラムを終了する前に glfwTerminate() 関数を実行する必要があります。main() 関数の最後の return 文の直前に glfwTerminate() 関数の呼び出しを追加します。

> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> glfwTerminate();  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
>   
> // ウィンドウが開いている間繰り返す  
> while (glfwWindowShouldClose(window) == GL_FALSE)  
> {  
> // ウィンドウを消去する  
> glClear(GL_COLOR_BUFFER_BIT);  
>   
> //  
> // ここで描画処理を行う  
> //  
>   
> // カラーバッファを入れ替える  
> glfwSwapBuffers(window);  
>   
> // イベントを取り出す  
> glfwWaitEvents();  
> }  
>   
> glfwTerminate();  
> }

#### 補足：atexit() による glTerminate() の実行

プログラムの終了時には必ず glTerminate() 関数を実行する必要があります。そのため、このプログラムでは main() 関数の最後の return 文の前のほか、glfwCreateWindow() 関数のエラー処理のところでも実行しています。

しかしプログラムを追加していくと、これら以外の場所でもプログラムを終了させなければならない場合が発生するかも知れません。そのようなとき、プログラムのあちこちで glTerminate() 関数を実行することは無駄に思われますし、呼び出しを忘れる可能性もあります。そこで、プログラムの終了時に必ず glTerminate() 関数が実行されるように、atexit() 関数を用います。

プログラムの先頭で atexit() 関数を定義しているヘッダファイル cstdlib を \#include し、glfwTerminate() 関数を実行する関数 cleanup() を定義します。そして glfwInit() 関数が成功した後で、atexit() 関数により cleanup() 関数を登録します。また、既に main() 関数に埋め込んでいた glfwTerminate() 関数は削除します。

> \#include \<cstdlib\>  
> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> // プログラム終了時の処理  
> static void cleanup()  
> {  
> // GLFW の終了処理  
> glfwTerminate();  
> }  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // プログラム終了時の処理を登録する  
> atexit(cleanup);  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
>   
> // ウィンドウが開いている間繰り返す  
> while (glfwWindowShouldClose(window) == GL_FALSE)  
> {  
> // ウィンドウを消去する  
> glClear(GL_COLOR_BUFFER_BIT);  
>   
> //  
> // ここで描画処理を行う  
> //  
>   
> // カラーバッファを入れ替える  
> glfwSwapBuffers(window);  
>   
> // イベントを取り出す  
> glfwWaitEvents();  
> }  
> }

int atexit(void (\*function)(void))

> atexit() 関数は、引数 functionに指定した関数を、プログラム終了時に実行するよう登録します。atexit() 関数を複数回呼び出して、複数の関数を登録することができます (少なくとも 32 個の関数が登録できます)。その場合、関数は登録した順の逆順に実行されます。戻り値として、関数の登録に成功した時は 0、失敗した時は 0 以外の値を返します。

### OpenGL のバージョンとプロファイルの指定

この講義では OpenGL 3.2 以降の機能を使用してプログラムを作成します。そのため、OpenGL のバージョンやプロファイルを指定してウィンドウを作成します。これは glfwCreateWindow() 関数でウィンドウを作成する前に、glfwWindowHint() 関数を用いて行います。

> 《省略》  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // プログラム終了時の処理を登録する  
> atexit(cleanup);  
>   
> // OpenGL Version 3.2 Core Profile を選択する  
> glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);  
> glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 2);  
> glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);  
> glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
>   
> 《省略》

void glfwWindowHint(int target, int hint)

> この後に glfwCreateWindow() 関数によって作成するウィンドウの特性を設定します。デフォルトの設定に戻すには glfwDefaultWindowHints() を呼び出します。
>
> target

ヒントを設定する対象。以下のものが指定できます (一部を抜粋)。

GLFW_RED_BITS, GLFW_GREEN_BITS, GLFW_BLUE_BITS, GLFW_ALPHA_BITS

それぞれカラーバッファの赤色・緑色・青色・アルファに割り当てるビット数を hint に指定します。デフォルトはいずれも 8 です。

GLFW_DEPTH_BITS

デプスバッファに割り当てるビット数を hint に指定します。デフォルトは 24 です。

GLFW_STENCIL_BITS

ステンシルバッファに割り当てるビット数を hint に指定します。デフォルトは 8 です。

GLFW_SAMPLES

hint にマルチサンプル時のサンプル数を指定します。0 を指定するとマルチサンプルが無効になります。デフォルトは 0です。

GLFW_STEREO

hint に GL_TRUE を指定すればステレオモードになります。デフォルトは GL_FALSE です。これを GL_TRUE にできるかどうかは、ハードウェアに依存します。

GLFW_CLIENT_API

hint に GLFW_OPENGL_ES_API を指定すれば OpenGL ES の API を使用します。デフォルトは GLFW_OPENGL_API です。

GLFW_CONTEXT_VERSION_MAJOR

OpenGL のメジャーバージョン番号を hint に指定します。バージョンが 3.2 ならば 3 です。デフォルトは 1 です。

GLFW_CONTEXT_VERSION_MINOR

OpenGL のマイナーバージョン番号を hint に指定します。バージョンが 3.2 ならば 2 です。デフォルトは 1 です。

GLFW_OPENGL_FORWARD_COMPAT

OpenGL の Forward Compatible Profile (前方互換プロファイル、古い機能が使えない) を使う場合は、hint に GL_TRUE を指定します。デフォルトは GL_FALSE です。

GLFW_OPENGL_PROFILE

使用する OpenGL のプロファイルを指定します。Compatible Profile を使う場合は hint に GLFW_OPENGL_COMPAT_PROFILE、Core Profile を使う場合は hint に GLFW_OPENGL_CORE_PROFILE を指定します。デフォルトは 0 で、この場合はシステムの設定に依存します。

グラフィックスハードウェアが glfwWindowHint() 関数で指定した特性に対応していなければ、その後の glfwCreateWindow() 関数の実行は失敗してウィンドウは開かれません。

### 作成したウィンドウに対する設定

一方、作成したウィンドウに対する設定は、glfwCreateWindow() 関数によるウィンドウの作成に成功した後に行います。ここでは glfwSwapInterval() 関数によって、ダブルバッファリングにおけるバッファの入れ替えタイミングを設定します。

> 《省略》  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // プログラム終了時の処理を登録する  
> atexit(cleanup);  
>   
> // OpenGL Version 3.2 Core Profile を選択する  
> glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);  
> glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 2);  
> glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);  
> glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 作成したウィンドウに対する設定  
> glfwSwapInterval(1);  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
>   
> 《省略》

void glfwSwapInterval(int interval)

> ダブルバッファリングにおける、カラーバッファの入れ替えのタイミングを指定します。
>
> interval

少なくとも interval に指定した回数だけディスプレイの垂直同期タイミング (V-Sync、帰線消去期間) を待ってから、カラーバッファの入れ替えを行います。普通は 1 を指定します。0 を指定するとディスプレイの垂直同期タイミングを待たなくなるため、数値の上では fps (frame per second) が上昇しますが、完全な画面表示が行われるわけではありません。

### 補助プログラム

3.3.8 節において、OpenGL のバージョンとプロファイルに OpenGL 3.2 Core Profile を使うように設定したので、従来の OpenGL の固定機能が使えません。図形を描画するためには、シェーダプログラムを作成する必要があります。

加えて、プラットホームによってはグラフィックスハードウェアが備えているすべての機能の API を用意していない場合があります (Windows に標準搭載されている OpenGL はバージョン 1.1 までの API しか対応していません)。その場合は、グラフィックスハードウェアのドライバから足らない API のエントリポイントを取り出してくる必要があります。これには GLEW (The OpenGL Extension Wrangler Library, <http://glew.sourceforge.net>) という便利なライブラリがあるのですが、ここでは自前で準備することにします。

なお、Windows / Mac OS X / Linux でソースを共通化するためには他にも追加のコードが必要になりますが、ここではそれは本題ではないので、この部分を gg.cpp と gg.h という二つのファイルにまとめています。これらのファイルをソースファイルと同じディレクトリ (フォルダ) に置き、プロジェクトに追加してください。

また、これらの他にglext.h (<http://www.opengl.org/registry/api/glext.h>) もダウンロードして、ソースプログラムと同じディレクトリ (フォルダ) に入れてください。

#### 追加するファイル

- gg.cpp

- gg.h

- glext.h

そして \#include \<GL/glfw.h\> の一行を \#include "gg.h" と using namespace gg; の二行に置き換え、glfwInit() から glfwSwapInterval(1) までを ggInit() に置き換えてください。なお、ggInit() の引数は glfwOpenWindow() と同じで、デフォルト引数としてこれまでの設定と同じ (0, 0, 0, 0, 0, 0, 0, 0, GLFW_WINDOW) を与えています。

#### ソースプログラムの変更点

> \#include \<cstdlib\>  
> \#include \<iostream\>  
> \#include \<GLFW/glfw3.h\>  
>   
> // 補助プログラム  
> \#include "gg.h"  
> using namespace gg;  
>   
> // プログラム終了時の処理  
> static void cleanup()  
> {  
> // GLFW の終了処理  
> glfwTerminate();  
> }  
>   
> int main()  
> {  
> // GLFW を初期化する  
> if (glfwInit() == GL_FALSE)  
> {  
> // 初期化に失敗した  
> std::cerr \<\< "Can't initialize GLFW" \<\< std::endl;  
> return 1;  
> }  
>   
> // プログラム終了時の処理を登録する  
> atexit(cleanup);  
>   
> // ウィンドウを作成する  
> GLFWwindow \*const window(glfwCreateWindow(640, 480, "Hello!", NULL, NULL));  
> if (window == NULL)  
> {  
> // ウィンドウが作成できなかった  
> std::cerr \<\< "Can't create GLFW window." \<\< std::endl;  
> return 1;  
> }  
>   
> // 作成したウィンドウを OpenGL の処理対象にする  
> glfwMakeContextCurrent(window);  
>   
> // 作成したウィンドウに対する設定  
> glfwSwapInterval(1);  
>   
> // 補助プログラムによる初期化  
> ggInit();  
>   
> // 背景色を指定する  
> glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
>   
> // ウィンドウが開いている間繰り返す  
> while (glfwWindowShouldClose(window) == GL_FALSE)  
> {  
> // ウィンドウを消去する  
> glClear(GL_COLOR_BUFFER_BIT);  
>   
> //  
> // ここで描画処理を行う  
> //  
>   
> // カラーバッファを入れ替える  
> glfwSwapBuffers(window);  
>   
> // イベントを取り出す  
> glfwWaitEvents();  
> }  
> }

#### 補足：補助プログラムを使わない場合

この講義では補助プログラムの使用を前提に説明を行いますが、補助プログラムを用いないでプログラムを作成する場合は、次のように設定してください。

OpenGL 3.2 の Core Profile では、gluLookAt() などを含む GLU (OpenGL Utility) ライブラリのいくつかの機能が使えないので、GLU を使わないよう GLFW_NO_GLU を \#define します。

##### Windows

補助プログラムを使わない場合、OpenGL 1.2 以降の機能をアプリケーションプログラムから呼び出せるようにするためには、GLEW を使用すると便利です。glfwCreateWindow() で GLFW のウィンドウを開いた後、「補助プログラムによる初期化」を行っている ggInit() の代わりに、glewExperimental = GL_TRUE; という代入を行った後で glewInit() を呼び出してください。

> \#incoude \<GL/glew.h\>  
> \#incoude \<GLFW/glfw3.h\>  
>   
> ...  
>   
> // 補助プログラムによる初期化  
> glewExperimental = GL_TRUE;  
> if (glewInit() != GLEW_OK)  
> {  
> // エラーメッセージ等  
> return 1;  
> }

##### Mac OS X

Mac OS X では glfw3.h を \#include する前に GLFW_INCLUDE_GLCOREARB を \#define しておきます。また gl3ext.h も \#include しておきます。

> \#define GLFW_INCLUDE_GLCOREARB  
> \#include \<GLFW/glfw3.h\>  
> \#include \<OpenGL/gl3ext.h\>

##### Linux

Linux では X11 にグラフィックスハードウェアメーカーのプロプライエタリドライバがインストールされていることを前提にしています。C++ の場合は GL_GLEXT_PROTOTYPES も \#define しておくといいと思います。

> \#define GL_GLEXT_PROTOTYPES  
> \#include \<GLFW/glfw3.h\>  
> \#include \<GL/glext.h\>

以降では gg.h / gg.cpp の使用を前提に説明します。

## プログラムのビルドと実行

ソースプログラムをコンパイルしてオブジェクトプログラムを生成し、リンクによりオブジェクトプログラム同士やライブラリを結合して実行プログラムを生成する一連の作業をビルドと呼びます。これは簡単なプログラムであればコンパイラのコマンドを用いて実行することができますが、プログラムが複雑になるとコンパイラのコマンドだけでビルドするのは手間がかかります。そこで、統合開発環境や make コマンドなどの補助的な手段を用いてビルドします。

### Windows

Visual Studio 2013 でビルドするには、「ビルド」メニューから「ソリューションのビルド」を選んでください (図 61)。その下の「“プロジェクト名” のビルド」でも構いません。

図 61 Visual Studio 2013 によるプログラムのビルド

プログラムの実行は、「デバッグメニュー」の「デバッグ開始」を選ぶか、ファンクションキーの F5 をタイプしてください。ツールバーにある「緑色の右向き三角▶」をクリックしてもデバッグ実行を開始します。ソースプログラムの修正後、ビルドせずにプログラムを実行した時は、先にビルドを実行します。

なお、ソリューション構成が「Debug」のとき、ビルド時に「LINK : warning LNK4098: defaultlib 'MSVCRT' は他のライブラリの使用と競合しています。/NODEFAULTLIB:library を使用してください。」という警告が出ることがあります。これはここでは無視してください。GLFW をダイナミックリンクすれば、この警告を抑制できます。

### Mac OS X

Xcode では、左上の黒い右向き三角▶をクリックすれば、プログラムのビルドと実行を続けて行います (図 62)。Command キーを押しながら R のキーをタイプしても同様です。

図 62 Xcode によるプログラムのビルドと実行

コマンドラインでビルドする場合は、c++ コマンドに -I/usr/local/include -L/usr/local/lib -lglfw3 -framework Cocoa -framework IOKit -framework OpenGL -framework CoreVideo オプションを追加してください。‘%’ はシェルのプロンプトを表します。

> % c++ main.cpp -I/usr/local/include -L/usr/local/lib -lglfw3 \\  
> -framework Cocoa -framework IOKit -framework OpenGL -framework CoreVideo

さすがに長過ぎるので、Makefile を作って make コマンドを実行するのが賢明だと思います。Makefile を用意していれば、make コマンドを実行するだけです。

> % make

### Linux

Geany の場合は、「ビルド」メニューの「ビルド」を選んでください (図 63)。ビルドされたプログラムを実行するには、同じ「ビルド」メニューの「実行」を選んでください。これらはそれぞれファンクションキーの F9 と F5 でも実行できます。また、ツールバー上にも対応するボタンがあります。

図 63 Geany によるプログラムのビルドと実行

コマンドラインでビルドする場合は、c++ コマンドに -lGL -lglfw3 -lXi -lXrandr -lXxf86vm -lX11 -lrt -lpthread -lm オプションを追加してください。‘%’ はシェルのプロンプトを表します。

> % c++ main.cpp -lGL -lglfw3 -lXi -lXrandr -lXxf86vm -lX11 -lrt -lpthread -lm

長いので、Makefile を作って make コマンドを使用することを勧めます。Makefile を用意していれば、make コマンドを実行するだけです。

> % make
