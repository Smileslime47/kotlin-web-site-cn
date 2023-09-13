[//]: # (title: Kotlin 路线图)

<table>
    <tr>
        <td><strong>最后修改时间</strong></td>
        <td>2023 年 7 月</td>
    </tr>
    <tr>
        <td><strong>下次更新时间</strong></td>
        <td><strong>2023 年 12 月</strong></td>
    </tr>
</table>

欢迎来看 Kotlin 路线图！一窥 Kotlin 团队的工作重点。

## 关键优先事项

这个路线图的目标是给出一个大的图景。这里列出了我们的关键项目——我们专注于交付的最重要的事情：

* **K2 编译器**: 重写 Kotlin 编译器，针对速度、并行性与统一性进行优化。 它还能让我们引入许多预期的语言特性。
* **K2-based IntelliJ plugin**: much faster code completion, highlighting, and search, together with more stable code analysis.
* **Kotlin Multiplatform**: promote the technology to Stable by improving the toolchain stability and documentation, and ensuring compatibility guarantees.
* **Experience of library authors**: a set of documentation and tools helping to set up, develop, and publish Kotlin libraries.

## 以子系统划分的 Kotlin 路线图

To view the biggest projects we're working on, visit the [YouTrack board](https://youtrack.jetbrains.com/agiles/153-1251/current) or the [Roadmap details](#路线图详情) table.

If you have any questions or feedback about the roadmap or the items on it, feel free to post them to [YouTrack tickets](https://youtrack.jetbrains.com/issues?q=project:%20KT,%20KTIJ%20tag:%20%7BRoadmap%20Item%7D%20%23Unresolved%20) or in the [#kotlin-roadmap](https://kotlinlang.slack.com/archives/C01AAJSG3V4) channel of Kotlin Slack ([request an invite](https://surveys.jetbrains.com/s3/kotlin-slack-sign-up)).

### YouTrack 看板

Visit the [roadmap board in our issue tracker YouTrack](https://youtrack.jetbrains.com/agiles/153-1251/current) ![YouTrack](youtrack-logo.png){width=30}{type="joined"}

![Roadmap board in YouTrack](roadmap-board.png){width=700}

### 路线图详情

<table>
    <tr>
        <th>子系统</th>
        <th>当前聚焦</th>
    </tr>
    <tr>
        <td><strong>语言</strong></td>
        <td>
            <p><tip><a href="https://youtrack.jetbrains.com/issue/KT-54620" target="_blank">List of all upcoming language features</a></tip></p>
        </td>
    </tr>
    <tr>
        <td><strong>编译器</strong></td>
        <td>
            <list>
                <li>🆕 <a href="https://youtrack.jetbrains.com/issue/KT-60255" target="_blank">Promote K2 compiler to Stable</a></li>
                <li>🆕 <a href="https://youtrack.jetbrains.com/issue/KT-60276" target="_blank">Support debugging inline functions on Android</a></li>
                <li>🆕 <a href="https://youtrack.jetbrains.com/issue/KT-60277" target="_blank">Promote Kotlin/Wasm to Alpha</a></li>
                <li>🆕 <a href="https://youtrack.jetbrains.com/issue/KT-60278" target="_blank">Make Kotlin/Wasm suitable for standalone Wasm VMs</a></li>
            </list>
        </td>
    </tr>
    <tr>
        <td><strong>多平台</strong></td>
        <td>
            <list>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-55513">Promote Kotlin Multiplatform Mobile to Stable</a></li> 
                <li><a href="https://youtrack.jetbrains.com/issue/KT-55512">Improve the new Kotlin/Native memory manager robustness and performance and deprecate the old one</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-52600" target="_blank">Stabilize klib: make binary compatibility easier for library authors</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-42297" target="_blank">Improve exporting Kotlin code to Objective-C</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-42294" target="_blank">Improve Kotlin/Native compilation time</a></li>
            </list>
         </td>
    </tr>
    <tr>
        <td><strong>工具</strong></td>
        <td>
            <list>
                <li>🆕 <a href="https://youtrack.jetbrains.com/issue/KT-60279">Improve Kotlin build reports</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KTIJ-23988">First public release of K2-based IntelliJ plugin</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KTIJ-23989">Improve performance and code analysis stability of the current IDE plugin</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-55515">Expose stable compiler arguments in Gradle DSL</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-49511" target="_blank">Improve Kotlin scripting and experience with <code>.gradle.kts</code></a></li>
            </list>
         </td>
    </tr>
    <tr>
        <td><strong>库生态</strong></td>
        <td>
            <list>
                <li>🆕 <a href="https://youtrack.jetbrains.com/issue/KT-60280" target="_blank">Provide initial series of <code>kotlinx-io</code> releases</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-48011" target="_blank">Release <code>kotlinx-metadata-jvm</code> as Stable</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-49527" target="_blank">Promote <code>kotlinx-kover</code> to Stable</a></li>
                <li><a href="https://youtrack.jetbrains.com/issue/KT-48998" target="_blank">Release Dokka as Stable</a></li>
            </list>
            <p>Ktor and Exposed roadmaps:</p>
            <list>
                <li><a href="https://blog.jetbrains.com/ktor/2022/12/16/ktor-2023-roadmap/" target="_blank">Ktor framework roadmap</a></li>
                <li><a href="https://blog.jetbrains.com/kotlin/2023/08/exposed-moving-forward/" target="_blank">Exposed library roadmap</a></li>
            </list>
         </td>
    </tr>
</table>

> * This roadmap is not an exhaustive list of all things the team is working on, only the biggest projects.
> * There's no commitment to delivering specific features or fixes in specific versions.
> * We will adjust our priorities as we go and update the roadmap approximately every six months.
> 
{type="note"}

## 相对 2022 年 12 月版的变化

### 已完成

We've **completed** the following items from the previous roadmap:

* ✅ Language: [Introduce special syntax for `until` operator](https://youtrack.jetbrains.com/issue/KT-15613)
* ✅ Language: [Provide modern and performant replacement for `Enum.values()`](https://youtrack.jetbrains.com/issue/KT-48872)
* ✅ Language: [Design and implement a solution for `toString`, `equals` and `hashCode` on objects (data object)](https://youtrack.jetbrains.com/issue/KT-4107)
* ✅ Compiler: [Release K2 Beta](https://youtrack.jetbrains.com/issue/KT-52604)
* ✅ Compiler: [Fix issues related to inline classes on the JVM](https://youtrack.jetbrains.com/issue/KT-49514)
* ✅ Compiler: [Implement an experimental version of Kotlin/Wasm compiler backend](https://youtrack.jetbrains.com/issue/KT-46773)
* ✅ Tooling: [Provide better experience with Kotlin Daemon](https://youtrack.jetbrains.com/issue/KT-49532)
* ✅ Tooling: [Improve the performance of Gradle incremental compilation](https://youtrack.jetbrains.com/issue/KT-42309)
* ✅ Tooling: [Release the Experimental version of the Kotlin Notebooks IJ IDEA plugin](https://youtrack.jetbrains.com/issue/KTIJ-23990)
* ✅ Library ecosystem: [Release `kotlinx-coroutines` 1.7](https://youtrack.jetbrains.com/issue/KT-49529)
* ✅ Library ecosystem: [Improve `kotlinx-datetime` library](https://youtrack.jetbrains.com/issue/KT-42315)
* ✅ Library ecosystem: [Continue to develop and stabilize the standard library](https://youtrack.jetbrains.com/issue/KT-52601)

### 新增

We've **added** the following items to the roadmap:

* 🆕 Compiler: [Release Kotlin 2.0](https://youtrack.jetbrains.com/issue/KT-60255)
* 🆕 Compiler: [Support debugging inline functions on Android](https://youtrack.jetbrains.com/issue/KT-60276)
* 🆕 Compiler: [Promote Kotlin/Wasm to Alpha](https://youtrack.jetbrains.com/issue/KT-60277)
* 🆕 Compiler: [Make Kotlin/Wasm suitable for standalone Wasm VMs (without JavaScript support)](https://youtrack.jetbrains.com/issue/KT-60278)
* 🆕 Tooling: [Improve Kotlin build reports](https://youtrack.jetbrains.com/issue/KT-60279)
* 🆕 Library ecosystem: [Provide initial series of `kotlinx-io` releases](https://youtrack.jetbrains.com/issue/KT-60280)

### 已删除

We've **removed** the following items from the roadmap:

* ❌ Language: [Support non-local `break` and `continue`](https://youtrack.jetbrains.com/issue/KT-1436)
* ❌ Compiler: [Stabilize JVM-specific experimental features](https://youtrack.jetbrains.com/issue/KT-46770)
* ❌ Library ecosystem: [Stabilize and document `atomicfu`](https://youtrack.jetbrains.com/issue/KT-46786)
* ❌ Library ecosystem: [Improve KDoc experience](https://youtrack.jetbrains.com/issue/KT-55073)
* ❌ Library ecosystem: [Provide a Kotlin API guide for libraries authors](https://youtrack.jetbrains.com/issue/KT-55077)

> Some items were removed from the roadmap but not dropped completely. In some cases, we've merged previous roadmap items
> with the current ones.
>
{type="note"}

### 进行中

All other previously identified roadmap items are in progress. You can check their [YouTrack tickets](https://youtrack.jetbrains.com/issues?q=project:%20KT,%20KTIJ%20tag:%20%7BRoadmap%20Item%7D%20%23Unresolved%20)
for updates.