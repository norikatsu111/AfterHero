# AfterHero

## 概要<br>
Java学習3か月目の復習　オブジェクト指向を取り入れたRPGゲームを作成

## 環境<br>
#「eclipse」コンソール上で表示

## 機能<br>
### 5日の行動コマンド（５パターンから選択事に１つずつ減っていく）<br>

	public class ChiceAction {

		//行動のコマンド変数
		private String goCity;
		private String goWork;
		private String goChurch;
		private String goToolShop;
		private String goCastle;

		public ChiceAction() {
			this.goCity = "1,街に行く";
			this.goWork = "2,バイトする";
			this.goChurch = "3,教会に行く";
			this.goToolShop = "4,道具屋に行く";
			this.goCastle = "5,城に行く";

		}
		public void formerHeroAction(FormerHero fh,ChildGoblin cg,Dwarf w ,Monk mo,ToolShop ts,MilitaryPoliceA mpa,TemporaryLodging tl) {

		//行動の選択
			LinkedList<String> chice = new LinkedList<>();

			chice.add(goCity);
			chice.add(goWork);
			chice.add(goChurch);
			chice.add(goToolShop);
			chice.add(goCastle);

			//要素が１以下になるまで繰り返す
			while (chice.size() >= 1) {

				{//要素が０か元勇者のHPが０の場合は処理中断
				if (chice.isEmpty() || fh.getHp() <= 0)
					//処理を止める
					System.exit(0);

				}

				System.out.println("\n" + fh.getName()+"の行動を選択してください！");

				System.out.println("\n" + "\u001b[92m選択\u001b[00m" + chice);

				System.out.print("\n" + "\u001b[95m半角数字で選択してください\u001b[00m＞");

				//行動選択の入力を求める
				String numAction = new Scanner(System.in).nextLine();

				switch (numAction) {

				//街に行く

					case "1":
						//選択した入力をチェックする
						if (chice.contains(goCity)) {
							//街でのコマンドメソッド
							cg.talkFh(fh);
							//行動の選択を削除
							chice.remove(goCity);
							//馬小屋で休むメソッド
							tl.stayTemporaryLodging(fh);
							//元勇者のステータス確認
							fh.statusFormerHero();
							break;
						} else {
							System.out.println("\n" + "\u001b[94m☠☠入力が違います！もう１度入れてください！☠☠\u001b[00m");
							break;
						}

					case "2": //バイトする
						//選択した入力をチェックする
						if (chice.contains(goWork)) {
							//働くコマンドメソッド
							w.talkFh(fh);
							//行動の選択を削除
							chice.remove(goWork);
							//馬小屋で休むメソッド
							tl.stayTemporaryLodging(fh);
							//元勇者のステータス確認
							fh.statusFormerHero();
							break;
						} else {
							System.out.println("\n" + "\u001b[94m☠☠入力が違います！もう１度入れてください！☠☠\u001b[00m");
							break;
						}

					case "3"://教会に行く
						if (chice.contains(goChurch)) {
							//治療する
							mo.talkFh(fh);
							//行動の選択を削除
							chice.remove(goChurch);
							//馬小屋で休むメソッド
							tl.stayTemporaryLodging(fh);
							//元勇者のステータス確認
							fh.statusFormerHero();
							break;
						} else {
							System.out.println("\n" + "\u001b[94m☠☠入力が違います！もう１度入れてください！☠☠\u001b[00m");
							break;
						}

					case "4"://道具屋に行く
						if (chice.contains(goToolShop)) {
							//道具屋会話
							ts.talkFh(fh);
							//行動の選択を削除
							chice.remove(goToolShop);
							//馬小屋で休むメソッド
							tl.stayTemporaryLodging(fh);
							//元勇者のステータス確認
							fh.statusFormerHero();
							break;
						} else {
							System.out.println("\n" + "\u001b[94m☠☠入力が違います！もう１度入れてください！☠☠\u001b[00m");
							break;
						}

					case "5"://城に行く
						if (chice.contains(goCastle)) {
							//城に行くコマンドメソッド
							mpa.meetMilitaryPoliceA(fh);
							//行動の選択を削除
							chice.remove(goCastle);
							//馬小屋で休むメソッド
							tl.stayTemporaryLodging(fh);
							//元勇者のステータス確認
							fh.statusFormerHero();
							break;
						} else {
							System.out.println("\n" + "\u001b[94m☠☠入力が違います！もう１度入れてください！☠☠\u001b[00m");
							break;
						}

					default:
						System.out.println("\n" + "\u001b[94m☠☠入力が違います！もう１度入れてください！☠☠\u001b[00m");
						break;
					}
			}
		}
		public String getGoCity() {
			return goCity;
		}
		public void setGoCity(String goCity) {
			this.goCity = goCity;
		}
		public String getGoChurch() {
			return goChurch;
		}
		public void setGoChurch(String goChurch) {
			this.goChurch = goChurch;
		}
		public String getGoToolShop() {
			return goToolShop;
		}
		public void setGoToolShop(String goToolShop) {
			this.goToolShop = goToolShop;
		}
		public String getGoCastle() {
			return goCastle;
		}
		public void setGoCastle(String goCastle) {
			this.goCastle = goCastle;
		}
	}
### 大勢の敵への範囲攻撃（１対多）	
 
	public void attack(MilitaryPolice[] mp,LinkedList<MilitaryPolice> many) {

		System.out.print("\n"+super.getName()+"は\u001b[91mそのするどい爪で兵士たちを軽く払った。\u001b[00m");
		input.anythingPush();

		System.out.print("\n"+this.offensivePower+"のダメージ");
		input.anythingPush();

		do {
			//オーガの攻撃力ー憲兵の攻撃
			this.offensivePower -= mp[flag].getHp();
			//憲兵の死亡報告
			mp[flag].die();
			//憲兵の削除
			many.remove(mp[flag]);
			//憲兵の死亡した次の人から襲いかかる
			flag++;
			System.out.println("");
			//憲兵が０人になったらブレイク
			if (many.isEmpty()) {
			break;
			}
		//オーガの攻撃の威力が０になるダメージ
		} while (this.offensivePower > 0);

		//オーガの攻撃力再セット
		this.offensivePower += 500;

		//デバッグ
		//System.out.println(this.offensivePower());
	}
### 憲兵２６人分を作成
	
		//憲兵のインスタンスを26人分複製

		MilitaryPolice[] mp = new MilitaryPolice[26];

		//憲兵Aを配列に入れる
		mp[0] = mpa;

		for(int i=1;i<26;i++) {

		String[] policeNum = {"A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P","Q","R","S","T","U","V","W","X","Y","Z"};

		//憲兵の攻撃力を乱数で取得
		int rum =new Random().nextInt(10)+1;

		mp[i] = new MilitaryPoliceB("憲兵"+policeNum[i], 100, rum);

		}
