# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-02T13:10:01.917330+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×114 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-11-02T13:04:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T13:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×12  [2026-11-02T12:32:33]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-11-02T12:30:11]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T12:30:11]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CIRCUIT_BREAKER_TRIP  ×13  [2026-11-02T12:08:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×17  [2026-11-02T12:08:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-11-02T12:08:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T12:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 12 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T10:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-02T09:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ORPHAN_SCAN  ×1  [2026-11-02T06:00:13]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=34.1% ROI=0.94 (コスト 9,500/回収 8,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-02T06:00:13]
- key: `ROI_STAT|S00: n=174 hit%=30.5% hit_CI[Bonf]=[21.5,41.2]% ROI=0.83 ROI_boot95=[0.61,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-02T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=175 hit%=33.7% hit_CI[Bonf]=[24.3,44.6]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.43MB / last modified 2026-11-02T13:08:16.681297+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
 error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=6&jcd=03&hd=20261102: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-02 13:08:02,695 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=6&jcd=03&hd=20261102: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-02 13:08:13,903 [INFO] scraper: odds_win: 4/6 parsed
2026-11-02 13:08:13,904 [INFO] scraper: fetch_race 03/6: boats=6 odds=189/191
2026-11-02 13:08:13,907 [INFO] predictor: CALIBRATION_MODE=on
2026-11-02 13:08:13,907 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-11-02 13:08:13,911 [INFO] run_cycle: fetched 03/6 [final]: 154 combos
2026-11-02 13:08:15,146 [INFO] race_id: notif: nid=2026110203061309 sid=S02_TETSUBAN phase=final rank=B
2026-11-02 13:08:15,530 [INFO] notifier: Discord notify OK (status=204)
2026-11-02 13:08:16,656 [INFO] notifier: Discord notify OK (status=204)
2026-11-02 13:08:16,684 [INFO] run_cycle: FINAL S02_TETSUBAN 江戸川6R B
2026-11-02 13:08:46,339 [INFO] scraper: odds3t: 120/120 parsed
2026-11-02 13:08:56,411 [INFO] scraper: odds3f: 20/20 parsed
2026-11-02 13:09:05,636 [INFO] scraper: odds2t: 30/30 parsed
2026-11-02 13:09:05,637 [INFO] scraper: odds2f: 15/15 parsed
2026-11-02 13:09:14,711 [INFO] scraper: odds_win: 4/6 parsed
2026-11-02 13:09:14,712 [INFO] scraper: fetch_race 18/10: boats=6 odds=189/191
2026-11-02 13:09:14,715 [INFO] predictor: CALIBRATION_MODE=on
2026-11-02 13:09:14,715 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-11-02 13:09:14,720 [INFO] run_cycle: fetched 18/10 [final]: 154 combos
2026-11-02 13:09:25,926 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=04&hd=20261102: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-02 13:09:54,390 [INFO] scraper: odds3t: 120/120 parsed

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 21
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 21
  }
]
```

## Phase別通知記録 (24h)
{'final': 5, 'result': 3, 'scan': 13}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 303
  FINAL_MISSING: 114
  CIRCUIT_BREAKER_NO_ACTION: 28
  ANOMALY_SCAN_FINAL_RATIO: 21
  CIRCUIT_BREAKER_TRIP: 21
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 7 | 9,300 | 5,550 | -3,750 | 0.597 |
| S01_NAKAANA1 | 27 | 7 | 5,400 | 4,260 | -1,140 | 0.789 |
| S02_TETSUBAN | 13 | 4 | 2,600 | 3,840 | +1,240 | 1.477 |

## 直近アラート (24h・新しい順)
```
[13:04:16] FINAL_MISSING: {"deadline": "2026-11-02T12:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110202051234", "sid": "S00"}
[13:04:16] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 461}
[13:00:35] CIRCUIT_BREAKER_TRIP: {"cost": 9300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 5550, "roi_7d": 0.597, "sid": "S00"}
[13:00:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 463}
[12:55:06] FINAL_MISSING: {"deadline": "2026-11-02T11:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110214071121", "sid": "S00"}
[12:55:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 464}
[12:55:06] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.473, "baseline_mean": 0.616, "baseline_stdev": 0.312, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.143, "today_scan_count": 7, "z_score": -1.52}
[12:52:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 463}
[12:48:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 455}
[12:46:19] FINAL_MISSING: {"deadline": "2026-11-02T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110202021112", "sid": "S00"}
```

## 本日残レース: 64件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 56件 締切済
- 通知発射: scan=7 nid / final=2 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 036R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 13:08:13 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 11:47:38 |
| S02_TETSUBAN | 0711R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 20:05:24 |
| S00 | 1810R | win | 1 | 0.4111 | 15.0 | 6.17 | 300 | scan=12.0 drift=+25.0% | 13:06:12 |
| S00 | 224R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 12:13:13 |
| S00 | 022R | win | 1 | 0.2290 | 5.7 | 1.31 | 300 | scan=- drift=- | 11:11:18 |
| S00 | 243R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 16:23:14 |
| S00 | 153R | win | 1 | 0.3177 | 16.0 | 5.08 | 300 | scan=- drift=- | 16:05:49 |
| S01_NAKAANA1 | 242R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:54:24 |
| S00 | 048R | win | 1 | 0.5174 | 7.7 | 3.98 | 300 | scan=15.8 drift=-51.3% | 14:08:04 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 41 | +4.2% | -58.7% | +85.6% | 13 | 6 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 215.4s |
| **Latency** (scan→final max) | 221.5s |
| **Traffic** (notifications 24h) | 21 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 408 | 0.4778 | 0.3407 | +0.1371 | 🟡+29% | 0.2373 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4404 | 0.2982 | 0.2237 | 🔴-0.07 | 0.785 |
| S01_NAKAANA1 | win | 173 | 0.4872 | 0.3295 | 0.2408 | 🔴-0.09 | 0.828 |
| S02_TETSUBAN | win | 64 | 0.5525 | 0.4844 | 0.2640 | 🔴-0.06 | 1.086 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 146 | 0.4106 | 0.3082 | 🔴+0.1024 |
| 0.50+ | 240 | 0.5450 | 0.3833 | 🔴+0.1616 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 359 | 0.742 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-11-02T13:10:01.917330+09:00_