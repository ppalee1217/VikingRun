環境設定:
此遊戲使用Unity 2020.3.24f1 ver.以及Visual Studio 2017 運行
相容於Windows 10作業系統
----------------------------------------------------------------------
遊戲操作:
使用鍵盤按鍵W、A、S、D、空白鍵進行操作
"W"為角色前進、"A"為角色左移、"S"為角色後退、"D"為角色右移、"空白鍵"為角色跳躍
當遇到轉角時按下"A"左轉、按下"D"右轉
*NOTE*請注意！你只有一次轉彎機會
----------------------------------------------------------------------
遊戲玩法:
在此遊戲中路上會隨機生成盾牌與障礙物，請盡可能地蒐集盾牌並且存活
當掉下懸崖、撞到路障或是被後方的敵人抓住時遊戲結束
結算時的總分為存活時間與得到盾牌數的總和
----------------------------------------------------------------------
Bonus:
我的遊戲在生成硬幣時產生類似於原本TempleRun中的一直排硬幣，並且在此基礎上再隨機移動某些硬幣，回歸最原始的玩法又增添一些新意，讓玩法不再單一
public class LandScape : MonoBehaviour
{
    private CreateLandscape CreateLandscape;
    private int StoneRnd;
    [SerializeField] GameObject Coin;
    [SerializeField] GameObject Stone;
    Random rand = new Random();
    private GameObject coin1;
    private GameObject coin2;
    private GameObject coin3;
    private GameObject stone;
    private void Start()
    {
        CreateLandscape = GameObject.FindObjectOfType<CreateLandscape>();
        for (int i = 0; i < 5; i++)
        {
            if ((rand.Next(0, 4) == 0))
            {
                stone = Instantiate(Stone, this.transform.Find("Coin" + Convert.ToString(rand.Next(1, 4))).GetChild(1));
            }
            coin1 = Instantiate(Coin, this.transform.Find("Coin1").GetChild(rand.Next(0, 3)));
            coin1.transform.localPosition += new Vector3(0, 0, 2f * i);
            coin2 = Instantiate(Coin, this.transform.Find("Coin2").GetChild(rand.Next(0, 3)));
            coin2.transform.localPosition += new Vector3(0, 0, 2f * i);
        }
        if (this.transform.Find("Coin3") != null)
        {
            for (int i = 0; i < 5; i++)
            {
                coin3 = Instantiate(Coin, this.transform.Find("Coin3").GetChild(rand.Next(0, 3)));
                coin3.transform.localPosition += new Vector3(0, 0, 2f * i);
            }
        }
    }
    private void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            CreateLandscape.Create();
            Destroy(CreateLandscape.ClearedScape);
        }
    }
}
----------------------------------------------------------------------
Feedback:
因為Unity只有三堂課，但是僅靠這三堂課真的很難學好怎麼使用工具，所以在寫這款遊戲時搞了很久也寫得拼拼湊湊的，希望此堂課應該關於這個部分可以再多上一點課。

GitHub專案網址:https://github.com/ppalee1217/VikingRun
