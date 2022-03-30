---
layout: page
title: VocaLiST
subtitle: An Audio-Visual Synchronisation Model for Lips and Voices
---

[comment]: <> (<div class="lead mb-0" align="justify" style="padding-bottom: 1em">)

[comment]: <> (The Y-Net model consist of a U-Net conditioned with visual features.  )

[comment]: <> (</div>)

[comment]: <> (![Y-Net]&#40;../img/model.png&#41;  )

[comment]: <> (<div class="lead mb-0" align="justify" style="padding-bottom: 1em">)

[comment]: <> (The system works with chunks of 4n seconds, where n ∈ N. The audio network takes as input a 256×16T n complex spectrogram and returns a complex mask.  The visual network in case of Y-Net-m and Y-Net-mr, is the video network &#40;in red&#41;, which takes as input a set of 100n frames cropped around the mouth of the target singer. In case of Y-Net-g and Y-Net-gr, the visual network is the graph network &#40;in green&#41; which takes as input a sequence of 68n landmarks of the face of the target singer. The visual features are fused with the audio network’s latent space through a FiLM layer &#40;we use T=16&#41;.  The FiLM broadcasts the 256×1×T visual features into the 256×16×T audio ones.  The spatial blocks of the U-Net downsample in both, the frequency and the temporal dimension, while the frequential block downsamples along the frequency dimension only.)

[comment]: <> (<br><br>)

[comment]: <> (Detailed layers are shown below. )

[comment]: <> (</div>)

[comment]: <> (<h3  style="padding-bottom: 10px"> U-Net structure </h3>)

[comment]: <> (<table>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>Block #</td>)

[comment]: <> (        <td>Type of block</td>)

[comment]: <> (        <td>Output channels</td>)

[comment]: <> (        <td>Kernel</td>)

[comment]: <> (        <td>Padding</td>)

[comment]: <> (        <td>Output shape</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <!--<tr>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>Input tensor</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>256 x 256</td>)

[comment]: <> (    </tr>-->)

[comment]: <> (    <tr>)

[comment]: <> (        <td>1</td>)

[comment]: <> (        <td>Spatial</td>)

[comment]: <> (        <td>32</td>)

[comment]: <> (        <td>5 x 5</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>128 x 128</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>Spatial</td>)

[comment]: <> (        <td>64</td>)

[comment]: <> (        <td>5 x 5</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>64 x 64</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>3</td>)

[comment]: <> (        <td>Spatial</td>)

[comment]: <> (        <td>128</td>)

[comment]: <> (        <td>5 x 5</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>32 x 32</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>4</td>)

[comment]: <> (        <td>Spatial</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>5 x 5</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>16 x 16</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>5</td>)

[comment]: <> (        <td>Frequential</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>5 x 5</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>8 x 16</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>6</td>)

[comment]: <> (        <td>Frequential</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>5 x 5</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>4 x 16</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>Bottleneck</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>3 x 3</td>)

[comment]: <> (        <td>1</td>)

[comment]: <> (        <td>8 x 16</td>)

[comment]: <> (    </tr>)

[comment]: <> (</table>)

[comment]: <> (<br>)

[comment]: <> (<h3  style="padding-bottom: 10px"> Video Network structure </h3>)

[comment]: <> (<table>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>Block #</td>)

[comment]: <> (        <td>Type of block</td>)

[comment]: <> (        <td>Output channels</td>)

[comment]: <> (        <td>Kernel</td>)

[comment]: <> (        <td>Padding</td>)

[comment]: <> (        <td>Stride</td>)

[comment]: <> (        <td>Output shape</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <!--<tr>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>Input tensor</td>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>-</td>)

[comment]: <> (        <td>100 x 100</td>)

[comment]: <> (    </tr>-->)

[comment]: <> (    <tr>)

[comment]: <> (        <td>0</td>)

[comment]: <> (        <td>Basic Stem</td>)

[comment]: <> (        <td>64</td>)

[comment]: <> (        <td>3 x 7 x 7</td>)

[comment]: <> (        <td>1 x 2 x 2</td>)

[comment]: <> (        <td>1 x 3 x 3</td>)

[comment]: <> (        <td>100 x 100</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>1</td>)

[comment]: <> (        <td>Spatio-temporal</td>)

[comment]: <> (        <td>64</td>)

[comment]: <> (        <td>3 x 3 x 3</td>)

[comment]: <> (        <td>1 x 1 x 1</td>)

[comment]: <> (        <td>1 x 1 x 1</td>)

[comment]: <> (        <td>100 x 100</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>Spatial</td>)

[comment]: <> (        <td>128</td>)

[comment]: <> (        <td>3 x 3</td>)

[comment]: <> (        <td>1 x 1</td>)

[comment]: <> (        <td>2 x 2</td>)

[comment]: <> (        <td>100 x 100</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>3</td>)

[comment]: <> (        <td>Spatial</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>3 x 3</td>)

[comment]: <> (        <td>1 x 1</td>)

[comment]: <> (        <td>2 x 2</td>)

[comment]: <> (        <td>100 x 100</td>)

[comment]: <> (    </tr>)

[comment]: <> (</table>)

[comment]: <> (<br>)

[comment]: <> (<h3 style="padding-bottom: 10px">Graph Network structure </h3>)

[comment]: <> (<table>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>Block #</td>)

[comment]: <> (        <td>Output channels</td>)

[comment]: <> (        <td>Output shape</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <!--<tr>)

[comment]: <> (        <td>Input tensor</td>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>100 x 68</td>)

[comment]: <> (    </tr>-->)

[comment]: <> (    <tr>)

[comment]: <> (        <td>1</td>)

[comment]: <> (        <td>32</td>)

[comment]: <> (        <td>100 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>2</td>)

[comment]: <> (        <td>32</td>)

[comment]: <> (        <td>100 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>3</td>)

[comment]: <> (        <td>64</td>)

[comment]: <> (        <td>50 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>4</td>)

[comment]: <> (        <td>64</td>)

[comment]: <> (        <td>50 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>5</td>)

[comment]: <> (        <td>128</td>)

[comment]: <> (        <td>25 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>6</td>)

[comment]: <> (        <td>128</td>)

[comment]: <> (        <td>25 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>7</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>13 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (    <tr>)

[comment]: <> (        <td>8</td>)

[comment]: <> (        <td>256</td>)

[comment]: <> (        <td>13 x 68</td>)

[comment]: <> (    </tr>)

[comment]: <> (</table>)
