# product-test
这是一个关于Allen作为产品测试工程师的经验文档，有一些自己在测试工作中的一些问题，思路和一些业务之外的成长记录


##### 20230306本周收获：
- 测试前需要确认每个模块的**版本号**，固件版本，每个固件版本存在的已知问题。
- 测试过程中要明确是升级固件之后的**功能全测**还是针对Bug Fix的**专门测试**（固件版本不一致的样机应该有单独的标志用来区分）


##### 20230313本周收获：
- APP开发后，调用的产品本身的一些接口，所以在一些显示上面可能会出先问题，例如在**app和产品本身同时操作的时候，信号的接受顺序是怎样的**，如果app在调节值是一个需要时间的事件（T > 0.5s）,那么就需要考虑一个问题了，产品的数值是**实时调整**还是只在**确定后发送信号并调整数值**。这个时候让机器和APP同时操作，可能就会有一些意想不到的情况发生了
- 在每一版固件发布并升级后，是需要进行一次完整的回归测试的，因为，在新功能发布的时候，其实会有一些地方，因为和别的功能存在冲突或者重复的情况，在实际的使用中可能会有意想不到的
 bug 出现
 
 
##### 20230320本周收获：
- 利用chatgpt学习测试的思路，黑盒测试的几个方法还有需要在实际测试过程中不断地去体会才能更好的理解
- 利用chatgpt编写测试报告：测试报告的目的是要向项目管理人员和开发人员等，传递测试信息，更好的了解产品**目前的状态**，要描述**概述，策略，结果**，还要写一个总体的**缺陷报告**
- 这种主要做的就是定了一个测试用例的模版**编号，标题，预置条件，数据，步骤，结果**这几项作为关键要素，关于这个方面其实我也遇到了一些小的问题，就是把一些做整个回归测试的前置条件放在预置条件中，后来沟通就决定把这些类似于外观，版本号电量等放在测试之前的说明中，然后预置条件就只需要写那一条测试项的简单的条件了，类似于，开机测试，那预置条件就是关机，不用太多。

**测试用例标题**
- 应该用一个完整的句子，并能呢个完整表达测试意图
- 描述方式：什么情况下，谁做了怎样的事，得到了怎样的结果
- 不要用测试数据的组合当测试用例标题
- 标题不要太长

**测试步骤**
- 应该避免引用别的用例
- 避免用笼统的词
- 重点描述测试步骤和测试目的，不那么相关的信息可以作为预置条件
- 测试步骤不要太多，[2,6]比较合适

**测试数据**
- 避免过多的用户接口信息
- 数据和步骤可以分开来
- 多个参数时，可以用一个参数的组合


#### 20230327本周收获
- 测试策略是一种选择，是一种在复杂情况下该如何进行测试的选择，是测试价值观的体现。比如说，在产品交付前，我会最关心市场最需要确认的特性是什么，分配比较大的精力去保证出镜率
比较高的特性能够尽可能稳定的状态。看到这边的时候就选择了去回顾一下从产品的角度去思考，会注重哪些方便。
- 功能性：在指定条件下试用能够比较完整的覆盖各种功能，并且能得到正确的结果
- 兼容性：与其他产品共享资源时互不影响试用，且能交换信息
- 安全性：
- 可靠性：
- 易用性：
- 效率：时间（响应，处理），资源，容量
- 可维护性：关于这个性质，最直观的就是可读取日志，升级不能影响业务，升级失败可退回
- 可移植性：


#### 20230403本周收获
- 当资源较多的时候，且同事会找自己借资源的时候，为了方便管理，第一件事是给资源分类，分一部分为可外借资源，一部分为自己使用的资源，这样即使更新的东西没有复原，外借资源数量不多的情况下也能很快复原。不容易出现混乱的情况。
- 单元测试是一种白盒测试，目的是把设计中的逻辑全部都跑一边，然后让结果和预期结果一致。这种测试更适合于开发人员自身。目前也想学习一些关于pytest或者其他的工具，来稍微熟悉熟悉白盒测试和自动化测试


#### 20230410本周收获
- 在遇到一个很难解决的问题，且很长时间没有解决（一个月以上）时，要做到先对系统边界明确，在逐渐缩小范围。一味的修改参数，只会导致，盲目行动，没有方向。
- 遇到一个新模块新功能的时候，在没有开发文档和需求文档做支撑的时候，可以先考虑按照提示，完整跑一边新功能，然后根据跑的过程中出现的模块，去猜测哪些部分可能出现bug

#### 20230417本周收获
- 在公司没有明确的测试用例集和整理过的需求文档时，首先要快速编写一份有完整测试项以及测试结果的测试用例集（之前测试时间偏多，测试用例编写时间偏少，零零散散），没有需求文档
的时候，需要快速写一份，有什么功能，各个功能都是用来干什么的文档，最快速的分类方式是，先把主要使用的特性分成一个大类，另外为了使用调试或者适配的东西分成另外一个大类，这样
可以快速分类，对主要功能特性的大类分配更多的时间。来面对多线程，任务急的情况
- 面对测试时间很短（半天时间），最主要的就是保证，最常使用的特性，最重要的功能正常，这样可以保证给同事出差前的产品是可用的，主要功能也是可用的，即使存在潜在的小bug，这些
还是在市场同事的可控范围以内
- 在产品交付的前期，可以根据整个产品的状态明确测试重点，比如说像现在公司某部门代码重构，且这是一个重要的部门，那么这个部门面临测试需求也是很高的，所以就可以分配大量的时间
对该部门有关的模块进行测试，帮助该部门找到更多的问题，这样才能从容的面对之后的挑战。尽量避免出现交付前，某模块因为时间紧张，测试时间不足，而导致bug频出。

#### 20230424本周收获
- 作为一个产品测试，或者现在更多的偏向产品，应该对价格敏感起来，需求去培养一些business sense。对某个配件，原材料分析，然后分析大概的成本价，在哪个范围内是可以接受的。可以多上1688看看厂商的价格，还有就是可以通过主要原料的厂商找到最原始的供应商
