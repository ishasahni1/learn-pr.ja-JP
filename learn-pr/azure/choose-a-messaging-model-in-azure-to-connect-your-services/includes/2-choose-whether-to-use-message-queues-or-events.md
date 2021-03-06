分散された音楽共有アプリケーションのアーキテクチャを計画しているとします。 アプリケーションでできるだけ高い信頼性とスケーラビリティを確保し、Azure テクノロジを使用して堅牢な通信インフラストラクチャを構築しようとしています。

適切な Azure テクノロジを選択するには、まずアプリケーションのコンポーネントが交わす個々の通信について理解しておく必要があります。 通信ごとに異なる Azure テクノロジを選択できます。

通信についてまず理解しなければならないのは、メッセージとイベントのどちらを送信するかということです。 Azure テクノロジには、イベントをターゲットとするものとメッセージをターゲットとするものがあり、これが基本的な選択肢となります。

## <a name="what-is-a-message"></a>メッセージとは何でしょうか。

分散アプリケーションの用語で、**メッセージ**には次の特性があります。

- メッセージには、1 つのコンポーネントによって生成され、別のコンポーネントで使用される生のデータが含まれています。
- メッセージには、データへの参照だけでなく、データ自体が含まれています。
- 送信側コンポーネントは、メッセージのコンテンツが宛先コンポーネントによって特定の方法で処理されることを想定しています。 システム全体の整合性は、特定のジョブを実行する送信側と受信側の両方によって決まる場合があります。

たとえば、ユーザーがモバイルの音楽共有アプリを使用して新しい曲をアップロードするとします。 モバイル アプリは、Azure で実行されている Web API にその曲を送信する必要があります。 新しい曲が追加されたことを示すアラートだけでなく、曲のメディア ファイル自体を送信する必要があります。 モバイル アプリは、Web API が新しい曲をデータベースに格納し、他のユーザーが利用できるようにすることを想定しています。 これはメッセージの例です。

## <a name="what-is-an-event"></a>イベントとは何でしょうか。

**イベント**はメッセージよりも軽量で、ほとんどの場合、ブロードキャスト通信に使用されます。 イベントを送信するコンポーネントは**発行元**と呼ばれ、受信側は**サブスクライバー**と呼ばれます。

イベントでは、一般的に受信側コンポーネントは対象の通信を決定し、それらの通信を "サブスクライブ" します。 通常、サブスクリプションは Azure Event Grid や Azure Event Hubs などの仲介役によって管理されます。 発行元がイベントを送信すると、仲介役は対象のサブスクライバーにそのイベントをルーティングします。 これは "発行/サブスクライブ アーキテクチャ" と呼ばれ、イベントを処理する唯一の方法ではありませんが、最も一般的です。

イベントには次の特性があります。

- イベントは、何かが発生したことを示す軽量の通知です。
- イベントは複数の受信側に送信される場合も、まったく送信されない場合もあります。
- 多くの場合、イベントは "ファンアウト" することを意図したり、発行元ごとに多数のサブスクライバーが存在します。
- イベントの発行元は、受信側コンポーネントが実行するアクションについて何も想定していません。
- 一部のイベントは個別のユニットであり、他のイベントに関連しません。 
- また、順序指定された関連するシリーズの一部であるイベントもあります。  

たとえば、音楽ファイルのアップロードが完了し、データベースに新しい曲が追加されたとします。 ユーザーに新しいファイルを通知するために、Web API は Web フロント エンドおよびモバイル アプリ ユーザーに新しいファイルを通知する必要があります。 ユーザーは、新しい曲を聴くかどうかを選択できます。つまり、最初の通知には音楽ファイルは含まれず、その曲が存在することをユーザーに通知するだけです。 送信側は、イベントの受信側がこのイベント受信に応答して特に何かを実行することは、想定していません。

これは、個別のイベントの例です。

## <a name="how-to-choose-messages-or-events"></a>メッセージまたはイベントを選択する方法

1 つのアプリケーションが、ある目的のためにイベントを使用し、別の目的のためにメッセージを使用するということはよくあります。 選択を行う前に、アプリケーションのアーキテクチャとそのすべてのユース ケースを分析して、そのコンポーネントが相互に通信する際のさまざまな目的をすべて識別する必要があります。 

イベントは、ブロードキャストに使用される可能性が高く、多くの場合に一時的です。つまり、通信が現在サブスクライブされていない場合、受信側で処理されない可能性があります。 メッセージは、分散アプリケーションで、通信の処理を保証する必要がある場合に使用される可能性が高くなります。

各通信について、送信側コンポーネントは通信が宛先コンポーネントによって特定の方法で処理されることを想定しているか、ということを問いかけてみてください。

答えが "はい" の場合は、メッセージを使用することを選択します。 答えが "いいえ" の場合は、イベントを使用できる可能性があります。

## <a name="summary"></a>まとめ

分散アプリケーションのコンポーネントは、さまざまな目的で相互に通信します。 これらの個々の目的について、その目的に合わせて設計された Azure テクノロジを選択するために、イベントとメッセージのどちらを使用するかを選択する必要があります。 

コンポーネントが通信する理由、およびイベントとメッセージのどちらを使用するかを理解しておくと、情報を交換するために Azure Storage キュー、Event Hubs、Event Grid、または Service Bus から選択する手順に進むことができます。