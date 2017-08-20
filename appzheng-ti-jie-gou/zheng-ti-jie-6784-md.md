## <a name="object">整体结构简介</a>
  
   + initDataModule 模块。
   > 本模块主要是调用app整体结构的数据描述 /json/crm_navigate/load-layout.action，此接口，和所有tab中默认tab的layoutWidgets数据。
   + main 模块
   > 本模块主要是注册所有页面级模块的Scene，方便通过Actions调用，以及把initDataModule传过来的数据做一下分发，分发给TabViewHolder模块。
   + NativeTabBar 模块
   > 此模块没有任何其他重要逻辑，主要是使用了第三方的tab结构，app所有的tab页面，即TabViewHolder模块都用此模块包裹了一下。主要是要符合router-flux的结构要求。
   + TabViewHolder 模块
   > 每一个tab的页面就是一个此模块，此模块是用来分发是否是ViewsPage的tab结构还是单个页面tab结构，以此来决定是使用ViewPagerWithIndicator模块还是ContainHolderView模块。当有悬浮在整个页面上的模块例如快捷操作按钮，就是在次模块中做处理。还有app中唯一的store应该是再次模块中注册生成才合适，但是现在是在ContainHolderView模块中进行了store的创建和reducer的合成，造成现在app是有多个store，后期会逐渐迁入到此模块中。
   + ViewPagerWithIndicator 模块 或者 ContainHolderView 模块
   > ViewPagerWithIndicator 模块本质是一个页面级的ViewPage，主要是用来处理当一个Tab页面是ViewPage结构时，用此模块来包裹，每个Page就是一个ContainHolderView模块。
   > ContainHolder模块，是我们app中单个页面的包裹模块，此模块现阶段拥有所有组件的reducer，所以当如果完成一个组件（非页面级组件）的开发的时候，要把组件的reducer在此模块中进行绑定。并且此模块还包含下拉刷新等页面刷新的操作也是放在此模块中。本质是一个ScrollView。
   
   流程图如下：
   
   ![](/assets/整体流程图.png)