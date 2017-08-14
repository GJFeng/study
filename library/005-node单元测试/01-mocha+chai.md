# [mocha](http://mochajs.org/) + [chai](http://chaijs.com/)
# 一、安装
##  测试框架mocha
在全局npm安装：    

    $ npm install --g mocha  
    
或作为您项目的开发依赖项：    

    $ npm install --save-dev mocha    
    
##  断言库 chai

    $ npm install --save-dev chai  
    
## TDD与BDD

#### TDD(测试驱动开发)
    suite('Array', function(){
    
         suiteSetup(function(){
             //suiteSetup will run only 1 time in suite Array, before all suite 
             console.log('suitSetup...');
         });
         
         setup(function(){
             //setup will run 1 time before every suite runs in suite Array
             console.log('setup...');
         });
     
         suite('indexOf()', function(){
             test('should return -1 when not present', function(){
                 assert.equal(-1, [1, 2, 3].indexOf(4));
             });
         });
     
         suite('indexOf2()', function(){
             test('should return not -1 when present', function(){
                 assert.equal(0, [1, 2, 3].indexOf(1));
             });
         });
    
         teardown(function(){
             //teardown will run 1 time after every suite runs in suite Array
             console.log('teardown...');
         });
     
         suiteTeardown(function(){
             //suiteTeardown will run 1 time in suite Array, after all suits run over.
             console.log('suiteTeardown...'); 
         });
     });
#### BDD(行为驱动开发)

    describe('Array',function(){
        describe('#concat()', function() {

            before(function () {
                // 在这个作用域的所有测试用例运行之前运行
            })
            
            beforeEach(function () {
                // 在这个作用域的每一个测试用例运行之前运行
            })
            it('should return 2 when given 2', function() {
                // 这个测试用例会运行
            });
            afterEach(function () {
                // 在这个作用域的每一个测试用例运行之后运行
            })
            after(function () {
                // 在这个作用域的所有测试用例运行完之后运行
            })
            
        })
    })
    

# 二、断言库比较

> -   `should.js` - BDD 风格贯穿始终      
> -   `expect.js` - expect() 风格的断言     
> -   `chai` - expect()、should和 assert()风格的断言    
> -   `better-assert` - C风格的自文档化的assert()    
> -   `unexpected` - “可扩展的BDD断言工具    

## chai接口

1. `should`     


    chai.should();
    
        foo.should.be.a('string');
        foo.should.equal('bar');
        foo.should.have.lengthOf(3);
        tea.should.have.property('flavors')
          .with.lengthOf(3);
          
2. `Expect`     
 

    var expect = chai.expect;

        expect(foo).to.be.a('string');
        expect(foo).to.equal('bar');
        expect(foo).to.have.lengthOf(3);
        expect(tea).to.have.property('flavors')
          .with.lengthOf(3);
         
3. `Asser`      
 

    var assert = chai.assert;

        assert.typeOf(foo, 'string');
        assert.equal(foo, 'bar');
        assert.lengthOf(foo, 3)
        assert.property(tea, 'flavors');
        assert.lengthOf(tea.flavors, 3);
        
##  [chai语言链](http://chaijs.com/api/bdd/)(BDD-->`expect`和`should`)
  提供以下内容作为可链接的`getter`，以提高您的断言的可读性。
- to
- be
- been
- is
- that
- which
- and
- has
- have
- with
- at
- of
- same
- but
- does   

## 
1. [`.not`](http://chaijs.com/api/bdd/#method_not)否定链中跟随的所有断言。   
 

    expect(function () {}).to.not.throw();   
    expect({a: 1}).to.not.have.property('b');    
    expect([1,2]).to.be.an('array').that.does.not.include(3);         


2. [`.property(name[, val[, msg]])`](http://chaijs.com/api/bdd/#method_property)断言目标具有给定键名称的属性。   
- **@param** _{ String }_ name    
- **@param** _{ Mixed }_ val (optional)
- **@param** _{ String }_ msg _ optional_ 


    expect({a: 1}).to.have.property('a');      

3. [`.equal(val[, msg])`](http://chaijs.com/api/bdd/#method_equal)断言目标是否全等于（===）等于给定的 ==val==。    
- **@param** _{ Mixed }_ val    
- **@param** _{ String }_ msg _ optional_  


    expect(1).to.equal(1);    
    expect('foo').to.equal('foo');
    
4. [`.eql(obj[, msg])`](http://chaijs.com/api/bdd/#method_eql)断言目标是等于（==）等于给定的 ==val==。    
- **@param** _{ Mixed }_ obj    
- **@param** _{ String }_ msg _ optional_   


    expect(1).to.equal(1);    
    expect('foo').to.equal('foo');
    
5. [`.a(type[, msg])`](http://chaijs.com/api/bdd/#method_a)断言目标的类型等于给定的字符串类型。类型不区分大小写。   
- **@param** _{ String }_ type    
- **@param** _{ String }_ msg _ optional_    


    expect('foo').to.be.a('string');
    expect({a: 1}).to.be.an('object');
    expect(null).to.be.a('null');
    expect(undefined).to.be.an('undefined');
    expect(new Error).to.be.an('error');
    expect(Promise.resolve()).to.be.a('promise');
    expect(new Float32Array).to.be.a('float32array');
    expect(Symbol()).to.be.a('symbol');
    
# 三、mocha
## 异步代码
在 `it()` 中添加一个回调`done`，当mocha测试完成后调用这个回调`done()`，通知mocha测试结束。否则，mocha就无法知道，会一直等到超时报错。


    it('测试应该5000毫秒后结束', function(done) {
        var x = true;
        var fn = function() {
            x = false;
            expect(x).not.ok;
            done(); // 通知Mocha测试结束
        };
        setTimeout(fn, 4000);
    });
上面的测试用例，需要4000毫秒之后，才有运行结果。所以，需要用`-t`或`--timeout`参数，改变默认的超时设置。
    
    $ mocha -t 5000 
    
Mocha默认会==高亮显示超过75毫秒==的测试用例，也可以用`-s`或`--slow`调整这个参数。

    $ mocha -t 5000 -s 1000
    
### promise
    
    it('异步请求应该返回一个对象', function() {
        return fetch('https://api.github.com')
            .then(function(res) {
                expect(res.json()).to.be.not.an('array');
            }).then(function(json) {

        });
    });

##

    promise.prototype.async=function (a) {
        return new Promise(function (resolve, reject) {
            fetch(a)
                .then(function(res) {
                    resolve(res)
                })
                .catch(function (err) {
                    reject(err)
                })
        })
    }
    it('异步请求应该返回一个对象', function(deno) {
        promise.async('https://api.github.com').then(function (res) {
            expect(res).to.be.not.an('array');
            deno()
        })
    });

    
## 钩子函数
钩子函数：`before()`,`after()`,`beforeEach()`,`afterEach()`。    
这些函数可以用来（在测试前）做预处理工作或在测试后清理工作。

    describe('hooks', function () {
        before(function () {
            // 在这个作用域的所有测试用例运行之前运行
        })
        
        after(function () {
            // 在这个作用域的所有测试用例运行完之后运行
        })
        
        beforeEach(function () {
            // 在这个作用域的每一个测试用例运行之前运行
        })
        
        afterEach(function () {
            // 在这个作用域的每一个测试用例运行之后运行
        })
        
          // 测试用例
    })
1. 测试用例和测试的钩子可以混合排列；    
2. `beforeEach()`,`afterEach()` ==每次测试用例== 开始运行前（结束后）都会执行；
3. `before()`,`after()` ==所有测试用例== (本作用域describe内)开始运行前（结束后）执行一次。
4. 相同的钩子函数按照书写顺序依次运行；
5. 整体的运行顺序：`before()`(一次)，`beforeEach()`，测试用例，`afterEach()`（循环运行），`after()`（一次）；

## 命令参数


> 命令 | 注解
>  :----- | :-----
> -h, --help | 输出帮助信息
> -V, --version | 输出mucha版本
> -A, --async-only | 强制让所有测试用例必须使用callback或者返回promise的方式来异步判断正确性
> -c, --colors | 启用报告中颜色
> -C, --no-colors | 禁用报告中颜色
> -G, --growl | enable growl notification support
> -O, --reporter-options <k=v,k2=v2,...> | reporter-specific options
> -R, --reporter <name> | specify the reporter to use
> -S, --sort | 排序测试文件
> -b, --bail | bail after first test failure
> -d, --debug | enable node's debugger, synonym for node --debug
> -g, --grep <pattern> | 只执行满足 <pattern>格式的用例
> -f, --fgrep <string> |                 只执行含有 <string> 的用例
> -gc, --expose-gc |                       展示gc回收的log
> -i, --invert |                          让 --grep 和 --fgrep 的匹配取反
> -r, --require <name> |                   require一下<name>指定的模块
> -s, --slow <ms>  |                       指定slow时间（单位ms，默认75ms）
> -t, --timeout <ms> |                     指定超时时间（单位ms，默认2000ms）
> -u, --ui <name> |                        指定user-interface (bdd|tdd|exports)
> -w, --watch    |                         观察用例文件变化，并重新执行
> --check-leaks  |                         检测未回收global变量泄露
> --compilers <ext>:<module>,... |         用指定的模块来编译文件
> --debug-brk |                            启用node的debug模式
> --delay |                                等待异步的用例集（见前边的）
> --es_staging |                           enable all staged features
> --full-trace |                           display the full stack trace
> --globals <names> |                      allow the given comma-delimited global [names]
> --harmony |                              enable all harmony features (except typeof)
> --harmony-collections |                  enable harmony collections (sets, maps, and weak maps)
> --harmony-generators |                   enable harmony generators
> --harmony-proxies  |                     enable harmony proxies
> --harmony_arrow_functions  |             enable "harmony arrow functions" (iojs)
> --harmony_classes  |                     enable "harmony classes" (iojs)
> --harmony_proxies  |                     enable "harmony proxies" (iojs)
> --harmony_shipping |                     enable all shipped harmony features (iojs)
> --inline-diffs  |                        显示预期和实际结果的string差异比较
> --interfaces   |                         display available interfaces
> --no-deprecation  |                      silence deprecation warnings
> --no-exit   |                            require a clean shutdown of the event loop: mocha will not call process.exit --no-timeouts |                          禁用timeout，可通过--debug隐式指定
> --opts <path> |                          定义option文件路径
> --prof |                                显示统计信息
> --recursive |                            包含子目录
> --reporters |                            展示可用报告
> --retries  |                             设置失败用例重试次数
> --throw-deprecation |                    每次调用deprecated函数的时候都抛出一个异常
> --trace |                                显示函数调用栈
> --trace-deprecation |                    启用的时候显示调用栈
> --watch-extensions <ext>,... |           --watch监控的扩展

1. --recursive  包含子目录
2. -t <time> 	超时时间（默认2000ms）
3. -R --reporter 参数用来指定测试报告格式，默认spec
4. --reporters 参数可以显示测试报告格式   
 
### mochawesome  测试报告格式


    npm install --save-dev mochawesome 
    
    mocha test.js --reporter mochawesome --reporter-options reportDir=aa,reportFilename=bb
        --reporter-options      通知 mochawesome 生成 HTML 格式选项
        reportDir               生成报告路径
        reportFilename	        报告文件名字
    
> Option | Name |	Type |	Default	Description
> ----|-------|----|----
> `reportDir` |	string |	[cwd]/mochawesome-report |	保存报告的路径t
> `reportFilename` |	string |	mochawesome |	保存的报告的文件名（在2.0.0之前称为`reportName`)
> `reportTitle` |	string |	mochawesome |	报告标题 
> `reportPageTitle` |	string |	mochawesome-report |    浏览器标题
> `inlineAssets` |	boolean |	false |内联报表资源 (scripts, styles)
> `enableCharts` |	boolean |	true |	显示套件图表
> `enableCode` |	boolean |	true    |	显示测试代码
> `enableTestCode` |	boolean |	true |	同`enableCode`弃用
> `autoOpen` |	boolean |	false |	运行测试后打开报告
> `overwrite` |	boolean |	true |	覆盖现有的报告文件
> `timestamp` |	string ||	以指定的格式追加时间戳来报告文件名. See [notes](https://github.com/adamgruber/mochawesome-report-generator/blob/master/README.md#timestamp).
> `showHooks` |	string |	failed|	设置挂钩的默认显示模式
> `quiet` |	boolean |	false |	静音控制台消息

# 引用
    
> [Mocha.js官方文档翻译 —— 简单、灵活、有趣](http://www.jianshu.com/p/9c78548caffa)    
> [测试框架 Mocha 实例教程——阮一峰](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)    
> [javascript单元测试框架mochajs详解](http://www.cnblogs.com/tzyy/p/5729602.html)    
> [mocha官网](http://mochajs.org/#installation)      
> [chai文档](http://chaijs.com/api/bdd/)      
> [用Mocha，Chai进行Node.js测试](http://webcache.googleusercontent.com/search?q=cache:http://www.html-js.com/article/1875&gws_rd=cr&ei=CbiLWdrnIIa10gTJ7YawCw)        