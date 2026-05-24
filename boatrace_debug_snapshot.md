# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-25T05:40:01.289375+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-05-24T23:08:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×52  [2026-05-24T23:08:06]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-05-24T20:01:05]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-05-24T19:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×34  [2026-05-24T12:26:29]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-05-24T08:59:22]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-24T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1288 actual=0.2000 gap=-0.0712`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-24T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-24T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=18.4% ROI=0.51 (コスト 10,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-24T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0041 actual=0.0769 gap=-0.0729`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-24T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.3333 gap=-0.1090`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-24T06:00:12]
- key: `ROI_STAT|S00: n=195 hit%=29.2% hit_CI[Bonf]=[20.8,39.3]% ROI=0.98 ROI_boot95=[0.73,1.27]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-24T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=195<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-24T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=70 hit%=31.4% hit_CI[Bonf]=[18.1,48.7]% ROI=0.82 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-24T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=70<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-24T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=44 hit%=45.5% hit_CI[Bonf]=[26.3,66.1]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-24T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=44<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-24T06:00:12]
- key: `ORPHAN_SCAN|239 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-24T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=48 hit%=33.3% ROI=0.89 (コスト 14,200/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-24T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=30.0% ROI=1.25 (コスト 9,500/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.39MB / last modified 2026-05-25T05:30:03.652228+09:00

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
02 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-24 23:55:06,402 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-24 23:55:06,545 [INFO] predictor: Models loaded OK
2026-05-24 23:55:06,549 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-24 23:56:05,431 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-05-24 23:56:05,431 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-24 23:56:05,431 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-24 23:56:05,499 [INFO] predictor: Models loaded OK
2026-05-24 23:56:05,502 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-24 23:57:05,962 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-05-24 23:57:05,962 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-24 23:57:05,962 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-24 23:57:06,006 [INFO] predictor: Models loaded OK
2026-05-24 23:57:06,010 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-24 23:58:05,553 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-05-24 23:58:05,553 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-24 23:58:05,555 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-24 23:58:05,614 [INFO] predictor: Models loaded OK
2026-05-24 23:58:05,618 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-24 23:59:05,865 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-05-24 23:59:05,865 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-24 23:59:05,865 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-24 23:59:05,946 [INFO] predictor: Models loaded OK
2026-05-24 23:59:05,952 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 13, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 252
  FINAL_MISSING: 63
  KS_ODDS_DRIFT: 41
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 2
  ANOMALY_SCAN_FINAL_RATIO: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 11 | 9,600 | 13,320 | +3,720 | 1.387 |
| S01_NAKAANA1 | 33 | 7 | 6,600 | 5,080 | -1,520 | 0.77 |
| S02_TETSUBAN | 14 | 6 | 2,800 | 1,800 | -1,000 | 0.643 |

## 直近アラート (24h・新しい順)
```
[23:56:05] FINAL_MISSING: {"deadline": "2026-05-24T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052409071322", "sid": "S02_TETSUBAN"}
[23:51:06] FINAL_MISSING: {"deadline": "2026-05-24T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052421020912", "sid": "S00"}
[23:28:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002935, "ks_stat": 0.231}
[23:23:05] FINAL_MISSING: {"deadline": "2026-05-24T08:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052421010846", "sid": "S00"}
[23:11:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:04:06] FINAL_MISSING: {"deadline": "2026-05-24T15:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052424011530", "sid": "S00"}
[23:01:06] FINAL_MISSING: {"deadline": "2026-05-24T09:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052423030924", "sid": "S00"}
[22:55:07] FINAL_MISSING: {"deadline": "2026-05-24T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052409071322", "sid": "S02_TETSUBAN"}
[22:50:09] FINAL_MISSING: {"deadline": "2026-05-24T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052421020912", "sid": "S00"}
[22:27:45] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002935, "ks_stat": 0.231}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 246R | win | 1 | 0.0295 | 10.3 | 0.30 | 300 | scan=4.0 drift=+157.5% | 17:47:21 |
| S01_NAKAANA1 | 244R | win | 1 | 0.5476 | 3.9 | 2.14 | 200 | scan=3.5 drift=+11.4% | 16:57:21 |
| S00 | 243R | win | 1 | 0.5123 | 6.9 | 3.53 | 300 | scan=6.8 drift=+1.5% | 16:27:22 |
| S01_NAKAANA1 | 013R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.6 drift=-13.9% | 16:24:22 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 12:52:21 |
| S01_NAKAANA1 | 115R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=3.1 drift=+54.8% | 12:26:20 |
| S00 | 218R | win | 1 | 0.0402 | 5.0 | 0.20 | 300 | scan=- drift=- | 12:02:31 |
| S00 | 238R | win | 1 | 0.4989 | 6.0 | 2.99 | 300 | scan=28.1 drift=-78.6% | 11:43:21 |
| S00 | 133R | win | 1 | 0.4989 | 40.5 | 20.21 | 300 | scan=35.2 drift=+15.1% | 11:35:22 |
| S01_NAKAANA1 | 132R | win | 1 | 0.5174 | 4.5 | 2.33 | 200 | scan=4.5 drift=+0.0% | 11:08:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +2.2% | -78.6% | +157.5% | 19 | 9 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 499.5s |
| **Latency** (scan→final max) | 603.9s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 311 | 0.4558 | 0.3055 | +0.1503 | 🟡+33% | 0.2323 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 190 | 0.4319 | 0.2789 | 0.2229 | 🔴-0.11 | 0.937 |
| S01_NAKAANA1 | win | 77 | 0.4837 | 0.2857 | 0.2429 | 🔴-0.19 | 0.747 |
| S02_TETSUBAN | win | 44 | 0.5098 | 0.4545 | 0.2540 | 🔴-0.02 | 0.827 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 15 | 0.0082 | 0.0667 | 🔴-0.0585 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 140 | 0.4201 | 0.2571 | 🔴+0.1629 |
| 0.50+ | 145 | 0.5405 | 0.3724 | 🔴+0.1681 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 20 | 0.744 |
| win | <5.0 | ✅learned | 38 | 0.802 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-25T05:40:01.289375+09:00_