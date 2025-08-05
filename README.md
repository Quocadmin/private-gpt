# PrivateGPT 

<a href="https://trendshift.io/repositories/2601" target="_blank"><img src="https://trendshift.io/api/badge/repositories/2601" alt="imartinez%2FprivateGPT | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

[![Tests](https://github.com/zylon-ai/private-gpt/actions/workflows/tests.yml/badge.svg)](https://github.com/zylon-ai/private-gpt/actions/workflows/tests.yml?query=branch%3Amain)
[![Website](https://img.shields.io/website?up_message=check%20it&down_message=down&url=https%3A%2F%2Fdocs.privategpt.dev%2F&label=Documentation)](https://docs.privategpt.dev/)
[![Discord](https://img.shields.io/discord/1164200432894234644?logo=discord&label=PrivateGPT)](https://discord.gg/bK6mRVpErU)
[![X (formerly Twitter) Follow](https://img.shields.io/twitter/follow/ZylonPrivateGPT)](https://twitter.com/ZylonPrivateGPT)

![Gradio UI](/fern/docs/assets/ui.png?raw=true)

PrivateGPT is a production-ready AI project that allows you to ask questions about your documents using the power
of Large Language Models (LLMs), even in scenarios without an Internet connection. 100% private, no data leaves your
execution environment at any point.

>[!TIP]
> If you are looking for an **enterprise-ready, fully private AI workspace**
> check out [Zylon's website](https://zylon.ai)  or [request a demo](https://cal.com/zylon/demo?source=pgpt-readme).
> Crafted by the team behind PrivateGPT, Zylon is a best-in-class AI collaborative
> workspace that can be easily deployed on-premise (data center, bare metal...) or in your private cloud (AWS, GCP, Azure...).

The project provides an API offering all the primitives required to build private, context-aware AI applications.
It follows and extends the [OpenAI API standard](https://openai.com/blog/openai-api),
and supports both normal and streaming responses.

The API is divided into two logical blocks:

**High-level API**, which abstracts all the complexity of a RAG (Retrieval Augmented Generation)
pipeline implementation:
- Ingestion of documents: internally managing document parsing,
splitting, metadata extraction, embedding generation and storage.
- Chat & Completions using context from ingested documents:
abstracting the retrieval of context, the prompt engineering and the response generation.

**Low-level API**, which allows advanced users to implement their own complex pipelines:
- Embeddings generation: based on a piece of text.
- Contextual chunks retrieval: given a query, returns the most relevant chunks of text from the ingested documents.

In addition to this, a working [Gradio UI](https://www.gradio.app/)
client is provided to test the API, together with a set of useful tools such as bulk model
download script, ingestion script, documents folder watch, etc.

## 🎞️ Overview
>[!WARNING]
>  This README is not updated as frequently as the [documentation](https://docs.privategpt.dev/).
>  Please check it out for the latest updates!

### Motivation behind PrivateGPT
Generative AI is a game changer for our society, but adoption in companies of all sizes and data-sensitive
domains like healthcare or legal is limited by a clear concern: **privacy**.
Not being able to ensure that your data is fully under your control when using third-party AI tools
is a risk those industries cannot take.

### Primordial version
The first version of PrivateGPT was launched in May 2023 as a novel approach to address the privacy
concerns by using LLMs in a complete offline way.

That version, which rapidly became a go-to project for privacy-sensitive setups and served as the seed
for thousands of local-focused generative AI projects, was the foundation of what PrivateGPT is becoming nowadays;
thus a simpler and more educational implementation to understand the basic concepts required
to build a fully local -and therefore, private- chatGPT-like tool.

If you want to keep experimenting with it, we have saved it in the
[primordial branch](https://github.com/zylon-ai/private-gpt/tree/primordial) of the project.

> It is strongly recommended to do a clean clone and install of this new version of
PrivateGPT if you come from the previous, primordial version.

### Present and Future of PrivateGPT
PrivateGPT is now evolving towards becoming a gateway to generative AI models and primitives, including
completions, document ingestion, RAG pipelines and other low-level building blocks.
We want to make it easier for any developer to build AI applications and experiences, as well as provide
a suitable extensive architecture for the community to keep contributing.

Stay tuned to our [releases](https://github.com/zylon-ai/private-gpt/releases) to check out all the new features and changes included.

## 📄 Documentation
Full documentation on installation, dependencies, configuration, running the server, deployment options,
ingesting local documents, API details and UI features can be found here: https://docs.privategpt.dev/

## 🧩 Architecture
Conceptually, PrivateGPT is an API that wraps a RAG pipeline and exposes its
primitives.
* The API is built using [FastAPI](https://fastapi.tiangolo.com/) and follows
  [OpenAI's API scheme](https://platform.openai.com/docs/api-reference).
* The RAG pipeline is based on [LlamaIndex](https://www.llamaindex.ai/).

The design of PrivateGPT allows to easily extend and adapt both the API and the
RAG implementation. Some key architectural decisions are:
* Dependency Injection, decoupling the different components and layers.
* Usage of LlamaIndex abstractions such as `LLM`, `BaseEmbedding` or `VectorStore`,
  making it immediate to change the actual implementations of those abstractions.
* Simplicity, adding as few layers and new abstractions as possible.
* Ready to use, providing a full implementation of the API and RAG
  pipeline.

Main building blocks:
* APIs are defined in `private_gpt:server:<api>`. Each package contains an
  `<api>_router.py` (FastAPI layer) and an `<api>_service.py` (the
  service implementation). Each *Service* uses LlamaIndex base abstractions instead
  of specific implementations,
  decoupling the actual implementation from its usage.
* Components are placed in
  `private_gpt:components:<component>`. Each *Component* is in charge of providing
  actual implementations to the base abstractions used in the Services - for example
  `LLMComponent` is in charge of providing an actual implementation of an `LLM`
  (for example `LlamaCPP` or `OpenAI`).

## 💡 Contributing
Contributions are welcomed! To ensure code quality we have enabled several format and
typing checks, just run `make check` before committing to make sure your code is ok.
Remember to test your code! You'll find a tests folder with helpers, and you can run
tests using `make test` command.

Don't know what to contribute? Here is the public 
[Project Board](https://github.com/users/imartinez/projects/3) with several ideas. 

Head over to Discord 
#contributors channel and ask for write permissions on that GitHub project.

## 💬 Community
Join the conversation around PrivateGPT on our:
- [Twitter (aka X)](https://twitter.com/PrivateGPT_AI)
- [Discord](https://discord.gg/bK6mRVpErU)

## 📖 Citation
If you use PrivateGPT in a paper, check out the [Citation file](CITATION.cff) for the correct citation.  
You can also use the "Cite this repository" button in this repo to get the citation in different formats.

Here are a couple of examples:

#### BibTeX
```bibtex
@software{Zylon_PrivateGPT_2023,
author = {Zylon by PrivateGPT},
license = {Apache-2.0},
month = may,
title = {{PrivateGPT}},
url = {https://github.com/zylon-ai/private-gpt},
year = {2023}
}
```

#### APA
```
Zylon by PrivateGPT (2023). PrivateGPT [Computer software]. https://github.com/zylon-ai/private-gpt
```

## 🤗 Partners & Supporters
PrivateGPT is actively supported by the teams behind:
* [Qdrant](https://qdrant.tech/), providing the default vector database
* [Fern](https://buildwithfern.com/), providing Documentation and SDKs
* [LlamaIndex](https://www.llamaindex.ai/), providing the base RAG framework and abstractions

This project has been strongly influenced and supported by other amazing projects like 
[LangChain](https://github.com/hwchase17/langchain),
[GPT4All](https://github.com/nomic-ai/gpt4all),
[LlamaCpp](https://github.com/ggerganov/llama.cpp),
[Chroma](https://www.trychroma.com/)
and [SentenceTransformers](https://www.sbert.net/).


1. PrivateGPT là gì?
PrivateGPT là một dự án mã nguồn mở giúp bạn hỏi và tương tác với AI về tài liệu cá nhân (file PDF, Word, text, v.v.) một cách riêng tư, không cần Internet. Tức là bạn có thể tải tài liệu vào hệ thống, rồi hỏi AI các câu hỏi liên quan, mà dữ liệu không bị gửi ra ngoài máy của bạn.

Thích hợp cho những ai quan tâm tới bảo mật và quyền riêng tư (ví dụ: công ty, ngành y tế, pháp lý).

Tất cả quá trình xử lý đều diễn ra trên máy tính cá nhân hoặc server nội bộ.

2. PrivateGPT hoạt động như thế nào?
Dự án này cung cấp một API (giao diện lập trình ứng dụng), giúp bạn xây dựng các ứng dụng AI riêng tư liên quan đến tài liệu. API này chia làm hai phần chính:

a. High-level API (Dễ dùng)
Tự động xử lý tài liệu: tải tài liệu lên, hệ thống tự động phân tích, chia nhỏ, tạo metadata, sinh embedding, lưu trữ, v.v.

Chat với AI về tài liệu: Hỏi đáp, tóm tắt, trích xuất thông tin dựa trên nội dung tài liệu đã nạp.

b. Low-level API (Nâng cao)
Cho phép lập trình viên can thiệp sâu vào từng bước như: sinh embedding, truy xuất các đoạn văn bản liên quan nhất cho một truy vấn.

3. Giao diện & Công cụ
Gradio UI: Có sẵn một giao diện web để bạn thử nghiệm hỏi đáp với AI về tài liệu.

Hỗ trợ nhiều công cụ khác như: script tải model hàng loạt, script nạp tài liệu, theo dõi thư mục tài liệu, v.v.

4. Tại sao lại có PrivateGPT?
Các mô hình AI lớn (LLM) rất hữu ích, nhưng nhiều doanh nghiệp/ngành nghề không dám dùng vì lo lộ dữ liệu.

PrivateGPT giúp mọi người tận dụng AI mà không phải chia sẻ dữ liệu cho bên thứ ba.

5. Kiến trúc bên trong
Sử dụng FastAPI để xây dựng API, tuân theo chuẩn API của OpenAI.

Dùng framework LlamaIndex cho các pipeline RAG (Retrieval Augmented Generation) – kết hợp AI và tìm kiếm dữ liệu trong tài liệu.

Các thành phần chính như LLM (mô hình AI), Vector Database, Embedding đều có thể thay đổi/dễ mở rộng.

Có sẵn code mẫu, kiến trúc rõ ràng, dễ mở rộng và đóng góp.

6. Tài liệu & Cộng đồng
Tài liệu chi tiết: https://docs.privategpt.dev/

Có Discord, Twitter, các nhóm cộng đồng để trao đổi và hỗ trợ.

7. Đóng góp & phát triển
Chào đón mọi đóng góp mã nguồn (PR, ý tưởng mới, sửa lỗi...).

Có bảng dự án công khai để theo dõi tiến độ, tính năng.

Nên kiểm tra code (make check) và test trước khi gửi PR.

8. Đối tác & Hỗ trợ
Dùng Qdrant (vector DB), Fern (tài liệu, SDK), LlamaIndex (pipeline AI).

Có cảm hứng/tích hợp từ các dự án nổi tiếng như LangChain, GPT4All, Llama.cpp, Chroma, SentenceTransformers.

9. Bạn có thể dùng PrivateGPT cho?
Tìm kiếm, hỏi đáp trên kho tài liệu công ty/cá nhân.

Tích hợp vào các ứng dụng nội bộ cần bảo mật thông tin.

Xây dựng chatbot AI riêng cho doanh nghiệp.

10. Tổng kết ngắn gọn
PrivateGPT = ChatGPT cho tài liệu cá nhân, chạy hoàn toàn cục bộ, cực kỳ bảo mật, dễ tích hợp, dễ phát triển thêm.
