# stndataprocess
433筆的資料為醫生使用探針從病人腦部由上往下電擊沿途不同區域所產生的訊號

資料的格式為smrx可使用spikeunterface套件打開

https://github.com/SpikeInterface/spikeinterface

取樣頻率24000Hz

檔案的名稱為病人+深度+區域

每筆資料打開長度sample數量為十八萬左右(39號病人只有三萬左右)

可使用以下程式碼打開

聽醫生說我們只會用到第一個channel所以後面用"0"

    import spikeinterface.extractors as 

    data = se.read_ced("./22/22_+0.442_SNr.smrx", "0")

    #parameter : 1. file_name, 2.channel id(str type)

    seq = data.get_traces()

    #then seq is the sequence of the channel in file.	


我們目標是協助醫生能夠辨識探針的所在位置，區分stn和非stn區，vental and dorsal 區域而找出最佳的手術位置

![螢幕擷取畫面 2022-07-14 135535](https://user-images.githubusercontent.com/77059184/181018370-fd5ed69b-e49b-4556-a7ef-c8fb6e56f8ad.png)

目前用一維cnn的架構來對一維資料做辨識

可以辨識stn和非stn區域達90%的準確率

但分類vental and dorsal 時只有60%左右

有些論文是有使用資料前處理的方式來增加辨識率

因此我們想試試看能不能先資料前處理再作分析

找出vental and dorsal 訊號特徵的差異



