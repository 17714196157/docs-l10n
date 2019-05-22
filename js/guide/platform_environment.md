# ƽ̨�ͻ���

TensorFlow.js�����ֹ���ƽ̨���������Node.js����ͬƽ̨�кܶ಻ͬ�����ã�ƽ̨��Ĳ���Ӱ���Ż���ƽ̨��Ӧ�ÿ�����

�������ƽ̨�ϣ�TensorFlow.js��֧���ƶ��豸��Ҳ֧��̨ʽ�豸����Ȼ�豸֮���кܶ���죬TensorFlow.js�ṩ��WebGL API�ܹ��Զ���Ⲣ����Ӧ���Ż����á�

��Node.jsƽ̨�ϣ�TensorFlow.js��֧��ֱ��ʹ��TensorFlow API��Ҳ֧�ָ�����CPU������

## [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#environments)����

��һ����TensorFlow.js�����ĳ�������ʱ�����е����ñ�ͳ��Ϊ������������һ��ȫ�ֵ�backend���Լ�һЩ���Ծ�ȷ����TensorFlow.js���Եı�ǡ�

### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#backends)Backends

TensorFlow.js֧�ֶ����ͬ��Backend������ʵ�ִ洢����ѧ�������κ�ʱ��ֻ��һ��backend��Ч���󲿷�ʱ�䣬TensorFlow.js����ݵ�ǰ�����Զ�ѡ��ʹ����ѵ�backend����ʹ����������Ȼ��Ҫ֪������ε�֪��ǰ����ʹ�õ����ĸ�backend���Լ�����ڲ�ͬbackend֮���л���

��������������ȡ��ǰ��ʹ�õ�backend

console.log(tf.getBackend());

�������������ֶ��л�backend

tf.setBackend(��cpu��);

console.log(tf.getBackend());
#### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#webgl-backend)WebGL backend

WebGL backend����ơ�webgl�������������ƽ̨����ǿ���һ��backend������CPU backendҪ��100��������ԭ���ǣ�Tensor����ΪWebGL������ģ���ѧ�������ʵ����WebGL shader���档

��������ʹ�����backendʱ��Ҫ�˽��һЩ֪ʶ��

##### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#avoid-blocking-the-ui-thread)��������UI�߳�
������һ����������tf.matMul(a,b)ʱ������ֵtf.Tensor��ͬ�����أ�Ȼ����ʱ����˷����㻹��һ����ɡ�����ζ�ŷ���ֵtf.Tensorֻ��һ��ָ������ľ����������x.data()��x.array()ʱ��ֻ�е��������ʱ����ȡ��ʵ��ֵ���������������У�Ϊ��������UI�̣߳���Ҫʹ���첽�汾��x.data()��x.array()��������ͬ���汾��x.dataSync()��x.arraySync()��
##### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#memory-management)�ڴ����

ǿ��һ�£���ʹ��WebGL backendʱ����Ҫ��ʽ�����ڴ档��Ϊ�洢Tensor��WebGL�������ᱻ������������ռ������Զ�����

����dispose()����tf.Tensorռ�õ��ڴ�
const a = tf.tensor([[1,2], [3,4]]);
a.dispose();

��Ӧ���У�������Ҫ�Ѷ���������������ά��һ���������м���������ã�Ȼ��������ռ�õ��ڴ棬���ַ���ʹ����ɶ��Ա�TensorFlow.js�ṩtf.tidy()��������������ʱ������Ҫ��tf.Tensor����ͺ�����ִ�к󣬱��ر������ᱻ����һ����

const a = tf.tensor([[1, 2], [3, 4]]);
const y = tf.tidy(() => {
  const result = a.square().log().neg();
  return result;
});

ע�⣺������WebGL��������Node.js TensorFlow backend��CPU backend�����Զ��������ջ��ƣ�����Щ������ʹ��dispose()��tidy()û�и����á�ʵ���ϣ���������ͨ������������յ�����������õ����ܡ�

##### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#precision)����

���ƶ��豸��WebGLֻ֧��16λ�������������Ȼ�����󲿷ֻ���ѧϰģ�Ͷ���32λ�����weight��activationѵ���ġ�����16λ��������ֻ�ܱ�ʾ[0.000000059605�� 65504]�����Χ������ģ����ֲ���ƶ��豸ʱ����������������⡣����Ҫ��֤�Լ�ģ���е�weight��activation��Ҫ���������Χ��
##### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#shader-compilation--texture-uploads)����Shader& texture �ϴ�
TensorFlow.js��GPU��ִ��WebGL��shader����Ȼ����Щshaderֻ���ڱ�����ʱ�Żᱻ���룬��lazy-compile�����������CPU�ϵ����߳���ɣ��⵼�³��������TensorFlow.js���Զ��������õ�shader���´��ٵ�����ͬ��shape��ͬ�����������tensorʱ�ܿ�ܶࡣTensorFlow.js������Ӧ��һ�����ʹ��ͬ���Ĳ�������˵ڶ������л��ܶࡣ

TensorFlow.js�����tf.Tensor���ݴ洢ΪWebGL������һ��tf.Tensor�������󣬲��ᱻ�����ϴ���GPU�����ǵ��䱻�õ�ʱ����ô����������tf.Tensor���ڶ���ʹ�ã������Ѿ���GPU����ʡ�����ϴ���������һ�����͵Ļ���ѧϰģ���У�����ζ��weight�ڵ�һ��Ԥ��ʱ���ϴ����ڶ��ξͻ��ܶࡣ

���ϣ���ӿ��һ��Ԥ������ܣ������Ƽ���ģ�ͽ���Ԥ�ȣ�������һ����ͬ��shape������Tensor��
����:
const model = await tf.loadLayersModel(modelUrl);
// Warmup the model before using real data.
const warmupResult = model.predict(tf.zeros(inputShape));
warmupResult.dataSync();
warmupResult.dispose();

// The second predict() will be much faster
const result = model.predict(userData);

#### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#nodejs-tensorflow-backend)Node.js TensorFlow backend

��Node.js TensorFlow backend�У�TensorFlow��C����API���������ٲ��������ᾡ����ʹ�û�����Ӳ������ģ�飬��CUDA��

�����backend�У���WebGL backendһ����������ͬ������tf.Tensor��Ȼ������WebGL backend��ͬ���ǣ����������tensor����ֵʱ�������Ѿ���ɡ�����ζ��tf.matMul(a,b)���û�����UI�̡߳�

��ˣ������������������ʹ���������������Ҫ�ڹ����߳��е��ã����������̡߳�

�������Node.js����Ϣ����鿴����ĵ���
#### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#cpu-backend)CPU backend

���backend����������backend��Ȼ������򵥵ġ����в�����ʵ����vanilla JavaScript�У���˺����в��л������һ�����UI�̡߳�

���backend�Բ������ã�����������WebGL����ʹ�õ��豸��

### [](https://github.com/tensorflow/tfjs-website/blob/master/docs/guide/platform_environment.md#flags)Flags

TensorFlow.js��һ�׻�����ǣ��ܹ��Զ������ͼ�⣬��֤�ǵ�ǰƽ̨�ϵ�������á���Щ��Ǵ󲿷����ڲ�ʹ�ã�������һЩȫ�ֱ�ǿ��Ա�API���ơ�

-   `tf.enableProdMode():`  ��������ģʽ������ȥ��ģ����֤��NaN��飬�Լ���������У��������Ӷ�������ܡ�
-   `tf.enableDebugMode()`: �����¼ÿ�ֲ�������־�������������̨������¼����������Ϣ�����ڴ�footprint���ں�ִ��ʱ�䡣ע���⽫���󽵵�Ӧ������ʱ�䣬����������������ʹ�á�

ע�������ַ���Ӧ���ڳ������ǰ����ã���Ϊ����Ӱ�����е�������ǡ�����ͬ����ԭ��û����Ӧ��disable������

ע�����б���ڿ���̨����¼Ϊtf.ENV.features������û�ж�Ӧ�Ĺ���API������Ҫ���ǰ汾���ݣ��������ʹ��tf.ENV.set���ı���Щ��ǣ��Ӷ��Գ�����΢������ϡ�