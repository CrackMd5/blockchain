A example c# api for https://www.blockchain.com/<br>
Request page:https://blockchain.info/multiaddr?active=$address|$address<br>
Api reference:https://www.blockchain.com/api/blockchain_api<br>


    program.cs
```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Net;
using System.Web.Helpers;

namespace BlockChain
{
    class Program
    {
        static void Main(string[] args)
        {
            string url = "https://blockchain.info/multiaddr?active=1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK|15EW3AMRm2yP6LEF5YKKLYwvphy3DmMqN6";
            string html = DownLoad(url);
            dynamic JSON = Json.Decode(html);

            foreach (var b in JSON.addresses)
            {
                string addr = b.address;
                int n_tx = b.n_tx;
                int final_balance = b.final_balance;
            }

            foreach (var tx in JSON.txs)
            {
                string txid = tx.hash;

                foreach (var o in tx.@out)
                {
                    string _addr = o.addr;
                }
            }
        }

        static string DownLoad(string url)
        {
            ServicePointManager.Expect100Continue = true;
            ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls
                   | SecurityProtocolType.Tls11
                   | SecurityProtocolType.Tls12
                   | SecurityProtocolType.Ssl3;

            string URI = url;
            HttpWebRequest request = WebRequest.Create(URI) as HttpWebRequest;
            request.KeepAlive = false;

            HttpWebResponse response = request.GetResponse() as HttpWebResponse;
            System.IO.Stream responseStream = response.GetResponseStream();
            System.IO.StreamReader reader = new System.IO.StreamReader(responseStream, Encoding.UTF8);
            string srcString = reader.ReadToEnd();
            return srcString;
        }
    }
}


```
    


My homepage : https://www.cmd5.org
