Javascript 代码片段
[JS]数组排序、求和、求平均数

let numbersArray = [5,8,6,99,55,22,44,77,75,65,45,54,51,105]
function compareNumbers(a, b){
  return a - b
}
//从小到大排序
numbersArray.sort(compareNumbers)
//数组求和
let sum = numbersArray.reduce((previous, current) => current += previous)
//求平均数
let avg = sum/numbersArray.length

[JS]数字转字母

function convert(num) {
    var result = [];
    while (num) {
        var t = num % 26;
        if (!t) {
            t = 26;
            --num;
        }
        result.push(String.fromCodePoint(t + 64));
        num = ~~(num / 26);
        console.log(num);
    }
    return result.reverse().join('');
}
console.log(convert(28));

[JS]多维数组扁平化

let myArray = [[1, 2],[3, 4, 5], [6, 7, 8, 9]]
let newArray= [].concat(...myArray)
console.log(newArray)
//[1, 2, 3, 4, 5,6, 7, 8, 9]

[JS]数组去重

let origin = ["22.247.176.5",
    "123.151.76.209",
    "61.148.245.120",
    "61.148.245.120",
    "61.148.245.128",
    "61.148.245.128",
    "61.148.245.148"];
let result = new Set();
let repeat = new Set();
origin.forEach(item => {
    result.has(item) ? repeat.add(item) : result.add(item);
});
console.log(Array.from(repeat));//去重后的数组
console.log(repeat);//找出重复的元素

[Nodejs]递归创建文件夹

const fs = require('fs');
fs.mkdirSync("D:\\2019\\2018\\2016\\2015\\2019", { recursive: true });

[JS]批量下载图片

const readline = require('readline');
const fs = require('fs');
const request = require('request');
var Bagpipe = require('bagpipe');
var async = require('async');
const rl = readline.createInterface({
    input: fs.createReadStream('bb.txt')
});
links = [];
var bagpipe = new Bagpipe(10);
fp = 'd:\\weibbb\\';
rl.on('line', (line) => {
    links.push(line);
}).on('close', function () {
    links.forEach((item, index) => {
        let filename = item.split('/').pop();
        bagpipe.push(saveImageFlie, item, fp + filename, function (err, data) {});
    });
});
const saveImageFlie = (src, dest, callback) => {
    request.head(src, function (err, res, body) {
        if (src) {
            request(src).on('error', function (err) {
                console.log(src + "   连接超时");
            }).pipe(fs.createWriteStream(dest)).on('close', function () {
                console.log('图片下载完成');
                callback(null, dest);
            });
        }
    });
};

[JS]合并bilibili下载视频

var fs = require('fs');
const {
    execSync
} = require('child_process');
var dir = "D:\\aa";
var allFiles = fs.readdirSync(dir);
const lua = "lua.flv.bb2api.80";
/**
 * 把blv改为flv，删除无关文件，准备input.txt以便用ffmpeg合并
 */
function bilibili() {    
    allFiles.forEach(function (el1) {
        let dir1 = dir + "\\" + el1;
        let dir2 = dir + "\\" + el1 + "\\" + lua;
        let filenum = 0;
        let inputstr = "";
        let allFile2 = fs.readdirSync(dir2);
        let i = 1;
        
        allFile2.forEach(function (filename) {
            if(filename.endsWith("blv")) {
                let newfilename = parseInt(filename.split(".")[0]) + 1;
                newfilename = newfilename + '.flv';
                inputstr = inputstr + "file '" + (i++) + ".flv'\n";
                fs.renameSync(dir2 + "\\" + filename, dir1 + "\\" + newfilename);
            }else {
                fs.unlinkSync(dir2 + "\\" + filename);
            }
        });
        fs.writeFileSync(dir1 + "\\input.txt", inputstr, function (err) {
            if(err) {
                console.log(err);
            }
            console.log("input.txt写入完成");
        });
        //删除无关文件
        if (fs.existsSync(dir1 + "\\danmaku.xml")) {
            fs.unlinkSync(dir1 + "\\danmaku.xml");
        }
        if (fs.existsSync(dir1 + "\\entry.json")) {
            fs.unlinkSync(dir1 + "\\entry.json");
        }
        fs.rmdirSync(dir2);        
    }, this);
}
/**
 * 把output.mp4改为第n集.mp4
 */
function changeOutputName() {
    allFiles.forEach(function (el, i) {
        fs.renameSync(dir + "\\" + el + "\\output.mp4", dir + "\\" + (i + 1) + ".mp4");
    });
}
/**
 * 使用ffmpeg把flv文件合成并转换为mp4
 */
function useFFmpeg() {
    allFiles.forEach(function(element){
        execSync("ffmpeg -f concat -i input.txt -c copy output.mp4", {
            cwd: dir + "\\" + element
        });
    });
}
// bilibili();
// useFFmpeg();
changeOutputName();



