# Cap-5-
from matplotlib import pyplot as plt
import signals as sigs
from matplotlib import style
from scipy import signal


#####################################################5.1 Signal to convolve###################################################################
##########################################################################################################################
style.use('ggplot')
f, plt_arr =plt.subplots(2,sharex=True)
f.suptitle("Input signal and impulse response")
plt_arr[0].plot(sigs.ecg_100Hz)
plt_arr[1].plot(sigs.Impulse_response)
plt.show()



f, plt_arr =plt.subplots(2,sharex=True)
f.suptitle("Input signal and impulse response")
plt_arr[0].plot(sigs.airflow_calibrated_100Hz)
plt_arr[1].plot(sigs.Impulse_response)
plt.show()
#######################################################5.2Convoluton########################################################
##########################################################################################################################
"""ecg_100Hz"""
output_signal = signal.convolve(sigs.ecg_100Hz,sigs.Impulse_response, mode='same')
style.use('ggplot')

f,plt_arr = plt.subplots(3,sharex=True)
f.suptitle("Convolution")
plt_arr[0].plot(sigs.ecg_100Hz, color ='cyan')
plt_arr[0].set_title("Input Signal")
plt_arr[1].plot(sigs.Impulse_response, color ='blue')
plt_arr[1].set_title("Impulse Response")
plt_arr[2].plot(output_signal, color ='magenta')
plt_arr[2].set_title("Output Signal")

plt.show()

"""airflow_calibrated_100Hz"""

output_signal = signal.convolve(sigs.airflow_calibrated_100Hz,sigs.Impulse_response, mode='same')

style.use('ggplot')

f,plt_arr = plt.subplots(3,sharex=True)
f.suptitle("Convolution")
plt_arr[0].plot(sigs.airflow_calibrated_100Hz, color ='cyan')
plt_arr[0].set_title("Input Signal")
plt_arr[1].plot(sigs.Impulse_response, color ='blue')
plt_arr[1].set_title("Impulse Response")
plt_arr[2].plot(output_signal, color ='magenta')
plt_arr[2].set_title("Output Signal")

plt.show()

#######################################################5.3Deconvoluton########################################################
##########################################################################################################################

sig = np.array([0,0,0,0,1,1,1,1])
filter = np.array([1,1,0])

conv_result = signal.convolve(sig,filter)
deconv_result = signal.deconvolve(conv_result,filter)

print("Convolution result :")
print(conv_result)
print("Deconvolution result : ")
print(deconv_result)

f,plt_arr = plt.subplots(3,sharex=True)
f.suptitle("convolution")
plt_arr[0].plot(sigs.ecg_100Hz, color ='cyan')
plt_arr[0].set_title("Input Signal")
plt_arr[1].plot(sigs.Impulse_response, color ='blue')
plt_arr[1].set_title("Impulse Response")
plt_arr[2].plot(output_signal, color ='magenta')
plt_arr[2].set_title("Output Signal")
plt.show()
#######################################################5.4Correlation########################################################
##########################################################################################################################

corr_output_signal = signal.correlate(sigs.ecg_100Hz, sigs.Impulse_response,mode ='same')
conv_output_signal = signal.convolve(sigs.ecg_100Hz, sigs.Impulse_response,mode ='same')

plt.plot(conv_output_signal)
plt.show()

corr_output_signal = signal.correlate(sigs.airflow_calibrated_100Hz, sigs.Impulse_response,mode ='same')
conv_output_signal = signal.convolve(sigs.airflow_calibrated_100Hz, sigs.Impulse_response,mode ='same')

plt.plot(conv_output_signal)
plt.show()
#######################################################5.6 Running Sum########################################################
##########################################################################################################################
output_signal = np.cumsum(sigs.ecg_100Hz)

#style.use('ggplot')
style.use('dark_background')

f,plt_arr = plt.subplots(2,sharex=True)
f.suptitle("Running Sum")

plt_arr[0].plot(sigs.ecg_100Hz,color='yellow')
plt_arr[0].set_title("Input Signal")

plt_arr[1].plot(output_signal,color ='magenta')
plt_arr[1].set_title("Output Signal")

plt.show()
##############################CODE#############################################################


def calc_running_sum(sig_src_arr,sig_dest_arr):
    for x in range(len(sig_dest_arr)):
        sig_dest_arr[x] = 0

    for x in range(len(sig_src_arr)):
        sig_dest_arr[x] = sig_dest_arr[x-1]+sig_src_arr[x]

        
    style.use('ggplot')
    #style.use('dark_background')

    f,plt_arr = plt.subplots(2,sharex=True)
    f.suptitle("Running Sum")

    plt_arr[0].plot(sig_src_arr,color='red')
    plt_arr[0].set_title("Input Signal")

    plt_arr[1].plot(output_signal,color ='magenta')
    plt_arr[1].set_title("Output Signal")

    plt.show()

output_signal =[None]*320
calc_running_sum(sigs.ecg_100Hz,output_signal)

#######################################################################################################################

output_signal = np.cumsum(sigs.airflow_calibrated_100Hz)

#style.use('ggplot')
style.use('dark_background')

f,plt_arr = plt.subplots(2,sharex=True)
f.suptitle("Running Sum")

plt_arr[0].plot(sigs.ecg_100Hz,color='yellow')
plt_arr[0].set_title("Input Signal")

plt_arr[1].plot(output_signal,color ='magenta')
plt_arr[1].set_title("Output Signal")

plt.show()
